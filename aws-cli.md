

```bash
aws --version
aws s3 ls
aws s3 ls s3://oiler
aws s3 mb s3://new-bucket
aws s3 rb s3://remove-bucket
aws s3 cp file.txt s3://my-bucket/ --grants read=uri=http://acs.amazonaws.com/groups/global/AllUsers
aws s3 cp <your directory path> s3://bucket-name --grants read=uri=http://acs.amazonaws.com/groups/global/AllUsers --recursive

```