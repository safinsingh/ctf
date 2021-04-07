# Description

Access the network service at url: `cfta-bx01.allyourbases.co` and port: `8012` and find a way to get the flag by formatting a valid request.

# Steps

Finally, an interesting description! Let's telnet in and see what we can find:

```
$ telnet cfta-bx01.allyourbases.co 8012
[...]
Processing request...
Exception: angle brackets not terminated.
hfdskjahfs
Error: Exception unresolved. Terminating.
[...]
```

Hmmm, interesting. Having recently been traumatized by the [Bastion of the Turbofish](https://github.com/rust-lang/rust/blob/master/src/test/ui/bastion-of-the-turbofish.rs) and reading C++ code, I knew exactly where to start. I figured I'd just spam `>` characters, but nothing seemed to really work. I ended up brute forcing a bunch of different lengths of `>` like so:

```rust
use tokio::{
    io::{AsyncReadExt, AsyncWriteExt},
    sync::mpsc,
    net::TcpStream,
};

const HOST: &str = "cfta-bx01.allyourbases.co:8012";

#[tokio::main]
async fn main() {
    let (tx, mut rx) = mpsc::channel::<String>(1);
    for i in 1..10000 {
        let tx = tx.clone();
        tokio::spawn(async move {
            let mut stream = TcpStream::connect(HOST).await.unwrap();
            stream
                .write_all((">".repeat(i) + "\n").as_bytes())
                .await
                .unwrap(); // you really thought i would add error handling?

            let mut bruh = String::new();
            stream.read_to_string(&mut bruh).await.unwrap();
            if !bruh.contains("unresolved") {
                tx.send(bruh).await.unwrap();
            }
        });
    }

    if let Some(s) = rx.recv().await {
        println!("{}", s);
    }
}
```

Sure enough, we get our flag:

```
Processing request...
Exception: angle brackets not terminated.
Request successful.

Flag: AlOnGSeaRcHFoROverWriTe
```
