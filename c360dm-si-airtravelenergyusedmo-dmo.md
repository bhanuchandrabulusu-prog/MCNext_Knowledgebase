# Air Travel Energy Use DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-airtravelenergyusedmo-dmo.html

---

Description: The date when the carbon footprint data of the associated stationary asset is due to be sent to a reporting body.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__Ch4PassengerKmInKgCo2eQty__c
Data Type: DOUBLE
Description: The CH4 emissions per kilometer that’s calculated based on the emission factor.
Field API Name: std__Ch4PassengerMileInKgCo2eQty__c
Data Type: DOUBLE
Description: The CH4 emissions per mile that’s calculated based on the emission factor.
Field API Name: std__Co2PassengerKmInKgQty__c
Data Type: DOUBLE
Description: The CO2 emissions per kilometer that’s calculated based on the emission factor.
Field API Name: std__Co2PassengerMileInKgQty__c
Data Type: DOUBLE
Description: The CO2 emissions per mile that’s calculated based on the emission factor.
Field API Name: std__CostCenterName__c
Data Type: TEXT
Description: The name of the cost center for the energy use record.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DestinationCityName__c
Data Type: TEXT
Description: The name of the destination city for the energy use record.
Field API Name: std__DestinationCountry__c
Data Type: TEXT
Description: The name of the destination country for the air travel of the energy use record.
Field API Name: std__EndDate__c
Data Type: DATEONLY
Description: The date when the values of the energy use record are no longer valid.
Field API Name: std__HaulLengthTxt__c
Data Type: TEXT
Description: The haul length calculated based on the segment distance and the haul-length of the associated emissions factor record.
Field API Name: std__Id__c
Data Type: TEXT
Description: The ID of the energy use record.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__IsRecordLockedInd__c
Data Type: BOOLEAN
Description: Indicates whether the waste footprint item record and the associated energy use records are locked for editing. The default value is ‘false’.
Field API Name: std__N2oPassengerKmInKgCo2eQty__c
Data Type: DOUBLE
Description: The N2O emissions per kilometer that’s calculated based on the emission factor.
Field API Name: std__N2oPassengerMileInKgCo2eQty__c
Data Type: DOUBLE
Description: The N2O emissions per mile that’s calculated based on the emission factor.
Field API Name: std__NameInterfaceField__c
Data Type: TEXT
Description: Name of this record.
Field API Name: std__Scope3CrbnFtprntId__c
Data Type: TEXT
Description: The scope 3 carbon footprint record for the energy use record.
Field API Name: std__Scope3EmissionsInTco2eQty__c
Data Type: DOUBLE
Description: The total scope 3 emissions in metric tonnes of carbon dioxide equivalent.
Field API Name: std__Scope3EmssnSrcId__c
Data Type: TEXT
Description: The scope 3 emission source for the energy use record.
Field API Name: std__SegmentDistanceInMilesQty__c
Data Type: DOUBLE
Description: The segment distance for this air travel record in miles.
Field API Name: std__SegmentDistanceNumber__c
Data Type: DOUBLE
Description: The segment distance for the air travel record.
Field API Name: std__SegmentDistanceUnitId__c
Data Type: TEXT
Description: The unit of measure for the segment distance.
Field API Name: std__SourceCityName__c
Data Type: TEXT
Description: The name of the source city for the air travel.
Field API Name: std__SourceCountry__c
Data Type: TEXT
Description: The name of the source country for the air travel.
Field API Name: std__StartDate__c
Data Type: DATEONLY
Description: The date when the values of the energy use record become valid.
Field API Name: std__SuplScope3EmissionsNumber__c
Data Type: DOUBLE
Description: The supplemental scope 3 emissions value that’s used to calculate the total scope 3 emissions.
Field API Name: std__SupplierId__c
Data Type: TEXT
Description: The ID of the supplier for the energy use record.
Field API Name: std__TravelerBaseCityName__c
Data Type: TEXT
Description: The name of the base city for the air traveler.
Field API Name: std__TravelerBaseCountry__c
Data Type: TEXT
Description: The name of the base country for the air traveler.
Field API Name: std__TravelerName__c
Data Type: TEXT
Description: The name of the traveler.
Field API Name: std__VendProvidedEmissionsInTco2eQty__c
Data Type: DOUBLE
Description: The scope 3 emissions provided by the vendor for the rental car booking or the aggregate details for multiple bookings. This emissions value overrides the calculated total scope 3 emissions.
