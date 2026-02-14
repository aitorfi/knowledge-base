---
layout: default
title: Form utils
parent: Dynamics 365 Finance & Operations
nav_order: 4
---

# Form utils

X++
{: .label .label-blue }

Snippet collection
{: .label .label-yellow }

## Snippets

The following snippet can be used to set the allowEdit property on all the fields in a form datasource.

```
[DataSource]
class ExampleDataSource
{
    public void setAllowEditOnAllFields(boolean _allowEdit)
    {
        DictTable dictTable = new DictTable(tableNum(ExampleDataSource));
        FieldId fieldId;

        fieldId = dictTable.fieldNext(0);
        while (fieldId)
        {
            FormDataObject formDataObject = this.object(fieldId);
            if (formDataObject)
            {
                formDataObject.allowEdit(_allowEdit);
            }
            
            fieldId = dictTable.fieldNext(fieldId);
        }
    }
}
```
