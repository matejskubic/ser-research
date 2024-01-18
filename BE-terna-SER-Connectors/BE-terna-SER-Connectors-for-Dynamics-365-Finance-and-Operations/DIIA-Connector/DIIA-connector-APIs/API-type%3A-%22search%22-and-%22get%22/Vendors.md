# D365FO Target data entity: `/data/VendorsV2`

#_API Methods_

##`POST`**/searchVendorMasterData**
Conducts a search for vendor master data.

## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. Unnecessary here, as only one record is eventually retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| Id | VendorAccountNumber |  |
| Date |  | Date (ISO 8601 format - "YYYY-MM-DD") for determining valid vendors |
| CompanyCode | LegalEntityId | Lowercase | 
| Email | PrimaryEmailAddress |
| IBAN | IBAN | IBAN stored in the vendor's bank details |
| Name | VendorOrganizationName | Vendor name. Wildcard search permitted. |
| OneTime |  | Restricts the search to one-time vendors or non-one-time vendors only. If this parameter is not specified, all vendors are taken into account in the search. |
| URL | PrimaryURL |   |
| VATNumber | TaxExemptNumber |

## Outbound data (searchVendorMasterDataResponse)
_The response arrives in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| VendorAccountNumber | Id |
| VendorOrganizationName | Name |
| PrimaryEmailAddress | Email |               |
| PrimaryURL | URL | |
| TaxExemptNumber | VATNumber |  |
| AddressValidFrom | Date| in the format "yyyy-MM-dd" |
| AddressStreet| Street | New line in the source data is replaced by a space character |
| AddressCity | City |
| AddressCountryRegionISOCode | Country |
| CompanyCode | dataAreaId | |
| IBAN | IBAN |

- Truncated (true or false, depending on whether all the data is displayed or not)

##`POST`**/getVendorMasterData**
Returns detailed information about the vendor that satisfies the filtering criteria.
## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. Unnecessary here, as only one record is eventually retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Id | VendorAccountNumber | Mandatory parameter |

## Outbound data (getVendorMasterDataResponse)
_The response as a single JSON object with the following format:_
| Source | Destination | Comment |
|--|--|--|
| dataAreaId | CompanyCode | |
| VendorAccountNumber | Id | |
| VendorOrganizationName | Name | |
| PrimaryContactEmail | Email | |
| PrimaryContactURL | URL | |
| StartDateOfBusiness | Date | in the format "yyyy-MM-dd" |
| AddressStreet | Street | New line in the source data is replaced by a space character |
| AddressCity | City |
| AddressZipCode | ZIP |
| AddressCountryRegionISOCode | Country |
| Name2 | null |
| POBox | null |
| POZIP | null |
| TAXNumber | null |
| VATNumbers | TaxExemptNumber | The output is a JSON array with just one element |
| Auxiliaries |  | JSON object consisting of:<ul><li>AlwaysWithPurchaseOrder, with a fixed boolean value false</li><li>AlwaysWithoutPurchaseOrder, with a fixed boolean value false</li></ul> |
| Bankdata | VendorBankAccounts | The output is a JSON array whose each element has the following fields:<table><tr><th>Source</th><th>Destination</th></tr><tr><td>bank.VendorBankAccountId</td><td>BankId</td></tr><tr><td>bank.BankName</td><td>BankName</td></tr><tr><td>bank.IBAN</td><td>IBAN</td></tr><tr><td></td><td>BIC (empty string)</td></tr></table>|
