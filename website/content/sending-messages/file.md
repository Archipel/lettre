#### File Transport

The file transport writes the emails to the given directory. The name of the file will be
`message_id.txt`.
It can be useful for testing purposes, or if you want to keep track of sent messages.

```rust
extern crate lettre;

use std::env::temp_dir;

use lettre::file::FileEmailTransport;
use lettre::{SimpleSendableEmail, EmailTransport};

fn main() {
    // Write to the local temp directory
    let mut sender = FileEmailTransport::new(temp_dir());
    let email = SimpleSendableEmail::new(
                    "user@localhost".to_string(),
                    &["root@localhost".to_string()],
                    "message_id".to_string(),
                    "Hello world".to_string(),
                ).unwrap();
    
    let result = sender.send(&email);
    assert!(result.is_ok());
}
```

Example result in `/tmp/b7c211bc-9811-45ce-8cd9-68eab575d695.txt`:

```text
b7c211bc-9811-45ce-8cd9-68eab575d695: from=<user@localhost> to=<root@localhost>
To: <root@localhost>
From: <user@localhost>
Subject: Hello
Date: Sat, 31 Oct 2015 13:42:19 +0100
Message-ID: <b7c211bc-9811-45ce-8cd9-68eab575d695.lettre@localhost>

Hello World!
```
