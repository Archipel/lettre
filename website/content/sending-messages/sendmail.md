#### Sendmail Transport

The sendmail transport sends the email using the local sendmail command.

```rust,no_run
extern crate lettre;

use lettre::sendmail::SendmailTransport;
use lettre::{SimpleSendableEmail, EmailTransport};

fn main() {
    let email = SimpleSendableEmail::new(
                    "user@localhost".to_string(),
                    &["root@localhost".to_string()],
                    "message_id".to_string(),
                    "Hello world".to_string(),
                ).unwrap();
    
    let mut sender = SendmailTransport::new();
    let result = sender.send(&email);
    assert!(result.is_ok());
}
```
