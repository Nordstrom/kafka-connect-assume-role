# kafka-connect-assume-role
A Kafka Sink Connector add-on that provides the ability to assume an AWS IAM role while writing to an AWS Resource such as S3 or SQS.

## Supported Kafka and AWS versions
The `kafka-connect-assume-role` add-on has been tested with `connect-api:2.1.0` and `aws-java-sdk-sqs:1.11.452`

# Building
You can build the connector with Maven using the standard lifecycle goals:
```
mvn clean
mvn package
mvn install
```

## Configuration

The kafka-connect-assume-role configuration requires these mandatory fields:
 * `<prefix>.class=com.nordstrom.kafka.connect.auth.AWSAssumeRoleCredentialsProvider`: The credentials provider class.
 * `<prefix>.role.arn`: The AWS IAM Role arn the connector will assume to write to the AWS Resource.
 * `<prefix>.session.name`: The session name.

The following fields are optional (but recommended) (see https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html):
 * `<prefix>.external.id`: An AWS IAM Role external identifier (to protect against confused deputy scenario)

### Sample Configuration

```json
{
  "config": {
    "connector.class": "io.confluent.connect.s3.S3SinkConnector",
    "flush.size": 1,
    "format.class": "io.confluent.connect.s3.format.bytearray.ByteArrayFormat",
    "key.converter": "org.apache.kafka.connect.converters.ByteArrayConverter",
    "key.converter.schemas.enable": false,
    "locale": "en",
    "partition.duration.ms": 600000,
    "partitioner.class": "io.confluent.connect.storage.partitioner.DefaultPartitioner",
    "rotate.schedule.interval.ms": 600000,
    "s3.acl.canned": "bucket-owner-full-control",
    "s3.credentials.provider.class": "com.nordstrom.kafka.connect.auth.AWSAssumeRoleCredentialsProvider",
    "s3.credentials.provider.role.arn": "arn:aws:iam::012345678901:role/my-restricted-role",
    "s3.credentials.provider.session.name": "my-session-name",
    "s3.credentials.provider.external.id": "my-external-id",
    "s3.bucket.name": "my-s3-bucket",
    "s3.compression.type": "none",
    "s3.part.size": 33554432,
    "schema.compatibility": "NONE",
    "storage.class": "io.confluent.connect.s3.storage.S3Storage",
    "tasks.max": 1,
    "timezone": "UTC",
    "topics": "my-s3-sink-topic",
    "topics.dir": "",
    "value.converter": "org.apache.kafka.connect.converters.ByteArrayConverter",
    "value.converter.schemas.enable": false
  },
  "name": "my-s3-sink"
}
```

## AWS IAM Assume Role and Policy

`TBD-TBD-TBD-TBD`

```json
```
