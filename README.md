# MongoDB Kafka connector customization

This implementaion allows the MongoDB Kafka sink connector to convert an existing _id that is string as ObjectId

# Build

./gradlew clean build

This will create a jar in build/libs/KakfaMongoHelper.jar

# Install

The KafkaMongoHelper.jar needs to be copied to the class lib in kafka, for example in /usr/share/java/kafka/, this is documented in kafka here:
https://docs.confluent.io/home/connect/community.html

# Usage

Once the plugin is installed in the worker you can configure the following properties to make it work in the connector:

If the id is provided as part of the value you can use:
```
		"post.processor.chain": "com.mongodb.kafka.connect.sink.processor.DocumentIdAdder",
		"document.id.strategy": "com.mongodb.kafka.connect.sink.processor.id.strategy.BsonOidProvidedInValueStrategy",
		"document.id.strategy.overwrite.existing": true,
```

If the id is provided as part of the key you can use:
```
		"post.processor.chain": "com.mongodb.kafka.connect.sink.processor.DocumentIdAdder",
		"document.id.strategy": "com.mongodb.kafka.connect.sink.processor.id.strategy.BsonOidProvidedInKeyStrategy",
		"document.id.strategy.overwrite.existing": true,
```

## Customization

The build file (`build.gradle.kts`) has a number of variables that can be changed to help customize the build.

```kts
val projectArchiveBaseName = "KafkaMongoHelper" // Set the outputted jar base name
val mongoKafkaConnectVersion = "1.6.1" // Set the mongo kafka connect version
val mongoDriverVersion = "[4.3,4.3.99)"
val kafkaConnectApiVersion = "2.6.0"
```

