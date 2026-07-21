# SFMC Tips #161 : Marketing Cloud Next: Segment Member Verification Agent

**Source:** https://medium.com/@marketingcloudtips/marketing-cloud-next-segment-member-verification-agent-18f64f4f22ba

---

# SFMC Tips #161 : Marketing Cloud Next: Segment Member Verification Agent

[![Nobuyuki Watanabe @marketingcloudtips](https://miro.medium.com/v2/resize:fill:64:64/1*zLRnWqPVgEgwGDwBBiwV3w.png)](/@marketingcloudtips?source=post_page---byline--18f64f4f22ba---------------------------------------)

[Nobuyuki Watanabe @marketingcloudtips](/@marketingcloudtips?source=post_page---byline--18f64f4f22ba---------------------------------------)

5 min read

·

Aug 15, 2025

--

Photo by [Joshua Hibbert](https://unsplash.com/@joshnh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

With the August 2025 Data Cloud release, the newly added **Member Verification Agent (Beta)** in the Segments feature enables you to quickly check whether a specific profile is included in a segment, leveraging **Agentforce**.

Previously, you had to either use the segment preview function in a flow or search via Data Explorer or Query Editor. Now, that extra effort is no longer necessary.

**From the Segment Builder or other screens, you can simply ask Agentforce** whether the specified profile is included in the segment. This allows you to quickly confirm membership and **reduce the risk of accidentally contacting unintended recipients**.

### **Requirements**

- Agentforce must be available in your environment.
- Agentforce credits will be consumed.
- The feature must be enabled in the Feature Manager.
- Since this is a beta version, in some environments, “Segment Member Validation” may not appear in the Asset Library.

## Setup Procedure

1. From **Setup**, search for **Feature Manager** and enable **Segment Member Validation (Beta)**.

2. Next, open **Agentforce (Default)** and click **Add from Asset Library**.

3. In the Asset Library, select **Segment Member Validation** and complete the process.

4. Once you have confirmed that **Segment Member Validation** has been added, enable **Agentforce (Default)**.

## **Understanding “Segment Member Validation”**

Let’s take a look at what the newly added topic **“Segment Member Validation”** does.

### **Topic Description**

**Classification Description**  
Questions to verify the Data Cloud segment accuracy, ensuring it contains the expected profiles.

**Scope**  
Your job is to verify whether the user input values exists within the segment.

**Instructions**

- Check whether the user has provided at least one `profile ID` to start the segment verification. If atleast one `profile ID` isn’t provided, prompt the user to enter one.
- Format the profile input as a list of `JSON elements`. Each element must include the `idValue`, which is the `profile ID`, with an optional `kQIdValue`, the key qualifier value.
- If the user provides a `segment name` or `ID`, use it as the `segmentIdentifier` for the `validateSegmentMember` action. If the user is on the record or Lightning page of the `MarketSegment` object, use the `currentRecordId` as the `segmentIdentifier` for the `validateSegmentMember` action. If the `segmentIdentifier` can’t be located, prompt the user to provide it.
- After extracting the relevant information, invoke the `validateSegmentMember` action.
- If the `validateSegmentMember` action returns only the `atLeastOneUserFound` output and no values in `errorMessage` or `nonErrorMessage`, respond to the user by stating whether at least one matching profile was found or not, based on the boolean value in `atLeastOneUserFound`.
- If `userMessage` isn’t empty, get back to the user with this message in conversational mode. If `errorMessage` isn’t empty, get back to the user that there was an error and reach out to Salesforce Support with the error code provided in the `errorMessage`.

### **Action Description**

**Validate Segment Member** (API: `validateSegmentMember`)

- Action Type: Flow

Checks whether the given profiles are present in the Data Cloud segment being built. Returns “Yes” (True) if the profiles are in the segment or “No” (False) if they aren’t.

## **How to Use the Agent**

### 1. When you are on the relevant segment page

1. Navigate to the target segment page in advance.

2. Open **Agentforce**.

3. Enter and execute text like the following:

`Is 003Kj00002ciXclIAE in this segment?`

4. Check the result. If the record exists, it will return **“True”** (Yes).

5. If the record does not exist, it will return **“False”** (No).

### 2. When you are not on the relevant segment page

1. From the **Marketing Cloud** home page, open **Agentforce**.

2. Enter and execute text like the following:

`Is 003Kj00002ciXclIAE in this segment?`

3. In this case, you will be asked for either the segment name or segment ID, so provide the information.

4. Check the result.

## Considerations

- Even if the segment target is **“Unified Individual”**, you can still search by **Salesforce ID**. However, at present, if multiple IDs are unified, the search result will return **False** (Not found). This is believed to be a bug and is expected to be fixed before the official release. ⚠️
- When the segment target is **“Unified Individual”**, searches cannot be performed using the Unified Individual ID.
- The search targets only the latest **published** state. If a segment has never been published, publish it first before searching.
- Simply applying filters and viewing the results will not make them searchable unless the final state has been published.
- In **older SDO (partner demo)** environments, internal errors may occur.

![]()

If you encounter the above error, give up and obtain a new SDO.  
 It seems that creating a case will not resolve the issue.

## **Final Note**

This feature is still in **beta**, so in **Marketing Cloud Next** segments that use Unified Individual profiles, there may be cases where some searches cannot be performed. Personally, I recommend first installing it into **Agentforce (Default)** for trial purposes, and then fully adopting it after these issues are resolved.

That’s all for now.

Stay tuned for more Salesforce Marketing Cloud tips! 😊

## Nobuyuki Watanabe

<https://www.linkedin.com/in/nobuyuki-watanabe/> (+Follow me)
