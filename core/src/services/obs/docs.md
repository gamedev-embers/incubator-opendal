## Capabilities

This service can be used to:

- [x] stat
- [x] read
- [x] write
- [x] create_dir
- [x] delete
- [x] copy
- [ ] rename
- [x] list
- [x] scan
- [x] presign
- [ ] blocking

## Configuration

- `root`: Set the work directory for backend
- `bucket`: Set the container name for backend
- `endpoint`: Customizable endpoint setting
- `access_key_id`: Set the access_key_id for backend.
- `secret_access_key`: Set the secret_access_key for backend.

You can refer to [`ObsBuilder`]'s docs for more information

## Example

### Via Builder

```rust
use anyhow::Result;
use opendal::services::Obs;
use opendal::Operator;

#[tokio::main]
async fn main() -> Result<()> {
    // create backend builder
    let mut builder = Obs::default();

    // set the storage bucket for OpenDAL
    builder.bucket("test");
    builder.endpoint("obs.cn-north-1.myhuaweicloud.com");
    // Set the access_key_id and secret_access_key.
    //
    // OpenDAL will try load credential from the env.
    // If credential not set and no valid credential in env, OpenDAL will
    // send request without signing like anonymous user.
    builder.access_key_id("access_key_id");
    builder.secret_access_key("secret_access_key");

    let op: Operator = Operator::new(builder)?.finish();

    Ok(())
}
```