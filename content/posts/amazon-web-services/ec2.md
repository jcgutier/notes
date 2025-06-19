- [Instance metadata](#instance-metadata)

# Instance metadata

We can retrieve instance metadata from an EC2 with `curl http://169.254.169.254/latest/meta-data/`

The launch templates have a security configuration to avoid multiple hops on a PUT call for metadata, on Terraform this can be set with:

```hcl
resource "aws_launch_template" "foo" {
  metadata_options {
    http_put_response_hop_limit = 1
  }
}
```
