# Attachments

We use attachments to store related documents for visit, activities, their reports and partner documents. This is a simple model which require file or hyperlink to be provided and has a simple generic foreign key, so it can be used everywhere.

The only interesting place here is the `code` field, which is used for generic relations to allow defining multiple reverse generic relations from one instance.

### CodedGenericRelation

Simple generic relation is limited to one relation between models, because it just set content type and instance pk. So we can't make multiple reverse relations to one generic, just like this:

```python
class MyModel(models.Model):
    attachments = GenericRelation(Attachment)
    report_attachments = GenericRelation(Attachment)
```

In this case both `MyModel.attachments.all()` and `MyModel.report_attachments.all()` will return identical set of attachments, because generic in fact don't create relation in the database. So we add code here, which will be used for filtering to separate attachments between defined relations.

```python
class MyModel(models.Model):
    attachments = CodedGenericRelation(Attachment, code='attachments')
    report_attachments = CodedGenericRelation(Attachment, code='report_attachments')
```

Now, if we save attachment with `code='attachments'`, it will appear only in `MyModel.attachments.all()`. `report_attachments` will be empty.

