# Impact of CMK states on API call {#concept_44211_zh .concept}

In Key Management Service \(KMS\), each Customer Master Key \(CMK\) has three states: Enabled, Disabled, and PendingDeletion. If the key is an **external key** \(when its Origin is EXTERNAL in KeyMetaData\), it may also be in the PendingImport state.

A new CMK is usually in the Enabled state by default. When creating a new **external key**, however, it is in the PendingImport state.

Only CMKs in the Enabled state can be used for encryption or decryption. Other APIs may return different responses depending on the key state.

CMKs in the PendingDeletion state are permanently deleted once the pre-deletion time runs out.

he following table shows key states and the expected responses of API calls.

|Expected responses|HttpStatusCode|
|:-----------------|:-------------|
|Success|200|
|Rejected.Enabled|409|
|Rejected.Disabled|409|
|Rejected.PendingDeletion|409|
|Rejected.PendingImport|409|
|Rejected.StateModifiedFailed|409|

|API|Enabled|Disabled|PendingDeletion|PendingImport|
|:--|:------|:-------|:--------------|:------------|
|CreateKey|Success|Success|Success|Success|
|GenerateDataKey|Success|Rejected.Disabled|Rejected.PendingDeletion|Rejected.PendingImport|
|Encrypt|Success|Rejected.Disabled|Rejected.PendingDeletion|Rejected.PendingImport|
|Decrypt|Success|Rejected.Disabled|Rejected.PendingDeletion|Rejected.PendingImport|
|ListKeys|Success|Success|Success|Success|
|DescribeKey|Success|Success|Success|Success|
|EnableKey|Success|Success|Rejected.StateModifiedFailed|Rejected.StateModifiedFailed|
|DisableKey|Success|Success|Rejected.StateModifiedFailed|Rejected.StateModifiedFailed|
|ScheduleKeyDeletion|Success|Success|Rejected.StateModifiedFailed|Success|
|CancelKeyDeletion|Rejected.StateModifiedFailed|Rejected.StateModifiedFailed|Success|Rejected.StateModifiedFailed|
|CreateAlias|Success|Success|Rejected.StateModifiedFailed|Success|
|DeleteAlias|Success|Success|Success|Success|
|ListAliases|Success|Success|Success|Success|

## Special API { .section}

**UpdateAlias**

-   It is affected only by the state of the “target key”, not the state of the “original key”.
-   If the “target key” is in the PendingDeletion state, Rejected.PendingDeletion is returned. If not, Success is returned.

**Exclusive API for the External Key**

|API|Enabled|Disabled|PendingDeletion|PendingImport|
|:--|:------|:-------|:--------------|:------------|
|GetParametersForImport|Success|Success|Success|Success|
|ImportKeyMaterial|Success|Success|Rejected.StateModifiedFailed|Success|
|DeleteKeyMaterial|Success|Success|Success|Success|

