# Introduction

The following snippet is used to retrieve individual dimension values from the DimensionAttributeValueCombination table.

```xpp
internal final class DimensionUtils
{
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
}
```xpp

The following snippet is used to get a default dimension with a modified dimension value.

```xpp
internal final class DimensionUtils
{
    public RecId replaceDefaultDimensionValue(DimensionValue _value, DefaultDimension _defaultDimension, Name _dimensionName)
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
            throw error(strFmt("@AVAFaros:AVAImportPayrollService_NoFinancialDimensionNameError", _dimensionName));
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
}
```xpp
