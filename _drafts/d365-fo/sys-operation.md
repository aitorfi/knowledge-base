# Introduction

The following example shows a simple SysOperation implementation featuring a multiselect company lookup and a custom regular lookup in the dialog.

## Contract

```xpp
[
    DataContract,
    SysOperationContractProcessing(classStr(ExampleUIBuilder))
]
internal final class ExampleContract extends SysOperationDataContractBase
{
    List selectedEntities;
    ProjId projId;

    [
        DataMember('selectedEntities'),
        SysOperationLabel("@SYS303247"),
        SysOperationDisplayOrderAttribute('1'),
        AifCollectionType('return', Types::String)
    ]
    public List parmSelectedLegalEntities(List _selectedEntities = selectedEntities)
    {
        selectedEntities = _selectedEntities;
        return selectedEntities;
    }

    [
        DataMember('projId'),
        SysOperationDisplayOrderAttribute('2')
    ]
    public ProjId parmProjId(ProjId _projId = projId)
    {
        projId = _projId;
        return projId;
    }
}
```

## UIBuilder

```xpp
internal final class ExampleUIBuilder extends SysOperationAutomaticUIBuilder
{
    ExampleContract contract;
    DialogField	availableCompanies;
    DialogField	projId;

    public void postBuild()
    {
        contract = this.dataContractObject() as ExampleContract;
        availableCompanies = this.bindInfo().getDialogField(contract, methodStr(ExampleContract, parmSelectedLegalEntities));
        projId = this.bindInfo().getDialogField(contract, methodStr(ExampleContract, parmProjId));

        availableCompanies.lookupButton(FormLookupButton::Always);
        projId.registerOverrideMethod(methodStr(FormStringControl, lookup), methodStr(ExampleUIBuilder, lookupProjId), this);
    }

    public void postRun()
    {
        Query query = new Query();
        QueryBuildDataSource qbdsLegalEntity = query.addDataSource(tablenum(CompanyInfo));

        qbdsLegalEntity.addSelectionField(fieldNum(CompanyInfo, DataArea));
        qbdsLegalEntity.addSelectionField(fieldNum(CompanyInfo, Name));

        container selectedFields = [tableNum(CompanyInfo), fieldNum(CompanyInfo, DataArea)];

        SysLookupMultiSelectCtrl::constructWithQuery(this.dialog().dialogForm().formRun(), availableCompanies.control(), query, false, selectedFields);
    }

    private void lookupProjId(FormStringControl _formStringControl)
    {
        Query query = new Query();
        QueryBuildDataSource qbds;
        SysTableLookup sysTableLookup;

        sysTableLookup = SysTableLookup::newParameters(tableNum(ProjTable), _formStringControl);
        
        query.allowCrossCompany(true);
        qbds = query.addDataSource(tableNum(ProjTable));

        sysTableLookup.addLookupfield(fieldNum(ProjTable, ProjId), true);
        sysTableLookup.addLookupfield(fieldNum(ProjTable, Name));
        sysTableLookup.addLookupfield(fieldNum(ProjTable, DataAreaId));
        sysTableLookup.parmQuery(query);
        sysTableLookup.performFormLookup();
    }
}
```

## Service

```xpp
internal final class ExampleService extends SysOperationServiceBase
{
    ProjId projId;
    List companies;

    public void process(ExampleContract _contract)
    {
        companies = _contract.parmSelectedLegalEntities();
        projId = _contract.parmProjId();

        ListEnumerator companiesEnumerator = companies.getEnumerator();
        while (companiesEnumerator.moveNext())
        {
            info(companiesEnumerator.current());
        }

        info(projId);
    }
}
```

## Controller

```xpp
internal final class ExampleController extends SysOperationServiceController
{
    protected void new()
    {
        super(classStr(ExampleService), methodStr(ExampleService, process));
    }

    public ClassDescription defaultCaption()
    {
        return "Example description of the process";
    }

    public ClassDescription caption()
    {
        return this.defaultCaption();
    }

    public static ExampleController construct(SysOperationExecutionMode _executionMode = SysOperationExecutionMode::Synchronous)
    {
        ExampleController controller;

        controller = new ExampleController();
        controller.parmExecutionMode(_executionMode);

        return controller;
    }

    public static void main(Args _args)
    {
        ExampleController controller;

        controller = ExampleController::construct();
        controller.parmArgs(_args);
        controller.startOperation();
    }

}
```
