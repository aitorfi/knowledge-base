---
layout: default
title: Dimension utils
parent: Dynamics 365 Finance & Operations
nav_order: 2
---

# Dimension utils

X++
{: .label .label-blue }

Snippet collection
{: .label .label-yellow }

## Snippets

The following snippet is used to retrieve individual dimension values from the DimensionAttributeValueCombination table.

```
public static DimensionValue getDimensionValue(DimensionAttributeValueCombination _davc, Name _dimensionName)
{
    DimensionAttribute dimensionAttribute = DimensionAttribute::findByName(_dimensionName);

    if (!dimensionAttribute)
    {
        // The given dimension does not exist.
        throw error(Error::wrongUseOfFunction(funcName()));
    }

    FieldId fieldId = DimensionAttributeValueCombination::getDimensionValueFieldId(dimensionAttribute.Name);
    return _davc.(fieldId);
}
```

The following snippet is used to get a default dimension with a modified dimension value.

```
public RecId replaceDefaultDimensionValue(DimensionValue _value, DimensionDefault _defaultDimension, Name _dimensionName)
{
    DimensionAttributeValue             dimAttrValue;
    DimensionAttribute                  dimAttr;
    DimensionAttributeValueSetStorage   davss;
    RecId                               defaultDimension = _defaultDimension;

    if (!_value)
    {
        return defaultDimension;
    }

    dimAttr = DimensionAttribute::findByName(_dimensionName);

    if (!dimAttr)
    {
        throw error(strFmt("Financial dimension '%1' not found.", _dimensionName));
    }

    dimAttrValue = DimensionAttributeValue::findByDimensionAttributeAndValue(dimAttr, _value, false, true);

    if (dimAttrValue)
    {
        davss = DimensionAttributeValueSetStorage::find(_defaultDimension);
        davss.addItem(dimAttrValue);
        defaultDimension = davss.save();
    }

    return defaultDimension;
}
```

The following snippet is used to merge 2 default dimension. If both default dimension contain a value for the same attribute the vale of the first default dimension will be taken.

```
public DimensionDefault mergeDimension(
    DimensionDefault _primaryDefaultDimension,
    DimensionDefault _secondaryDefaultDimension,
    DimensionDefaultMap _dimensionDefaultMap)
{
    return DimensionMerge::newFromTable(
        _dimensionDefaultMap,
        CompanyInfo::current()
    ).merge(_primaryDefaultDimension, _secondaryDefaultDimension);   
}
```

The following snippet is used to find or create a LedgerDiemnsion for a given MainAccount and DefaultDimension:

```
public LedgerDimensionAccount createLedgerDimensionFromMainAccountId(
    MainAccount                     _mainAccount,
    LedgerDefaultDimensionValueSet  _defaultDimensionRecId)
{
    return LedgerDimensionFacade::serviceCreateLedgerDimension(
        LedgerDefaultAccountHelper::getDefaultAccountFromMainAccountRecId(_mainAccount.RecId), _defaultDimensionRecId
    );
}
```
