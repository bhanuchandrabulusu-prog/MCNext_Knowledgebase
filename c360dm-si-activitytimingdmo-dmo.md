# Activity Timing DMO | Model Data in Data 360 | Data 360 DMO and Mapping Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-dmo-mapping/guide/c360dm-si-activitytimingdmo-dmo.html

---

Description: The number of minutes before or after the reference point specified in ActivityTime when the activity is performed.
Field API Name: std__ActivityTimeText__c
Data Type: TEXT
Description: A description of timing for a healthcare activity.
Field API Name: std__ActivityTimingText__c
Data Type: TEXT
Description: A code used to describe the Activity Timing.
Field API Name: std__ActivityTimingUsageType__c
Data Type: TEXT
Description: The type of activity the timing information is used for.
Field API Name: std__cdp_sys_record_currency__c
Data Type: TEXT
Description: System-generated metadata field that stores a 3-letter ISO currency code.
Field API Name: std__CountInPeriodNumber__c
Data Type: DOUBLE
Description: The recommended number of times the activity is performed in the specified period.
Field API Name: std__DataSourceId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__DataSourceObjectId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__Id__c
Data Type: TEXT
Description: Required. A unique, system-generated identifier for the ActivityTiming record. Maximum size is 36 characters.
Field API Name: std__InternalOrganizationId__c
Data Type: TEXT
Description: A unique, system-generated identifier for this record.
Field API Name: std__MaxActivityCountPerRepetitionQuantity__c
Data Type: DOUBLE
Description: The maximum number of repetitions allowed.
Field API Name: std__MaxActivityDurationQuantity__c
Data Type: DOUBLE
Description: The maximum length of time the activity is performed.
Field API Name: std__MaxCountInPeriodNumber__c
Data Type: DOUBLE
Description: The maximum number of times the activity is performed in the specified period.
Field API Name: std__MaxInPeriodCount__c
Data Type: DOUBLE
Description: Within a given period, the maximum number of times the activity is performed.
Field API Name: std__MaxRepetitionCycleLengthNumber__c
Data Type: DOUBLE
Description: For a single repetition, the maximum amount of time to complete the activity.
Field API Name: std__NameInterfaceField__c
Data Type: TEXT
Description: Name of this record.
Field API Name: std__PeriodEndDateTime__c
Data Type: DATETIME
Description: The date and time when the activity period ends.
Field API Name: std__PeriodLengthLowerLimitNumber__c
Data Type: DOUBLE
Description: The shortest period length to complete the activity.
Field API Name: std__PeriodLengthNumber__c
Data Type: DOUBLE
Description: A numeric description of the period length. The description is based on the Period unit of measure.
Field API Name: std__PeriodLengthUomid__c
Data Type: TEXT
Description: Alphanumeric string representing the period length uomid.
Field API Name: std__PeriodLengthUpperLimitNumber__c
Data Type: DOUBLE
Description: The shortest period length to complete the activity.
Field API Name: std__PeriodStartDateTime__c
Data Type: DATETIME
Description: The date and time when the activity period starts.
Field API Name: std__RepetitionCycleLengthNumber__c
Data Type: DOUBLE
Description: The suggested amount of time to complete a single repetition of the activity.
Field API Name: std__RepetitionCycleUomid__c
Data Type: TEXT
Description: Alphanumeric string representing the repetition cycle uomid.
Field API Name: std__TimingCodeId__c
Data Type: TEXT
Description: The interval for recurrences of the event. Valid values are Secondly, Minutely, Hourly, Daily, Weekly, Monthly, and Yearly.
Field API Name: std__WeeklyActivityTimeId__c
Data Type: TEXT
Description: The time, day or night, when the healthcare activity is to be performed.
