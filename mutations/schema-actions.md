---
description: Manage Schema Registry from within kPow
---

# Schema Registry

## Prerequisites

* You have setup the correct [access control permissions](../authorization/overview.md) in kPow to allow `SCHEMA_CREATE` and `SCHEMA_EDIT`
* You have configured [Schema Registry](../config/schema-registry.md) within kPow

## Creating Subjects

Topic create can be found in the navigation menu under the **Schema** menu item. Navigate to the **Create Subjects** button found within the Subjects table.

The form will allow you to create a new subject for schema type's `AVRO`,`JSON` or `PROTOBUF`. You can validate that the proposed schema is valid by clicking the **Validate Schema** button on the top right of the form.

![Creating a new subject](<../.gitbook/assets/out (5).gif>)

## Managing Subjects

### Editing Subjects

#### Compatibility 

You can change the compatibility of a subject by clicking the subject's row in the overview page and then clicking the **Change compatibility** button on the top right hand corner of the subject's form.

![Updating the compatibility of cc-value to BACKWARDS_TRANSITIVE](<../.gitbook/assets/out (4).gif>)



#### Versioning

You can make revisions to your subject's schema by clicking on the subject's row in the overview page and then making the change to the schema. You can validate the the revisions to the schema you are making are valid for the compatibility mode of your subject.

![Updating the schema for cc-value](<../.gitbook/assets/Screen Shot 2021-05-05 at 2.51.51 pm (1).png>)

### Deleting subjects

You can delete subjects by selecting the row(s) for the subjects you wish to delete, then clicking the **Delete (n) Subjects** button on the top right of the Subjects table.

 

![Deleting subjects from kPow's UI](<../.gitbook/assets/out (3).gif>)

### Cleaning up orphaned subjects

An orphaned subject is any subject with a naming strategy of `TopicNameStrategy` or `TopicRecordNameStrategy` that have no associated topic on your Kafka cluster. 

kPow will detect any orphaned subjects inside your schema registry and prompt you to clean them up within the **Schema** UI:

![Orphaned subject detection](<../.gitbook/assets/Screen Shot 2021-05-05 at 2.39.25 pm.png>)
