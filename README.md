# Zoho-CRM-Data-Formatting-Automation-Deluge-Script
Zoho CRM automation using Deluge script to format and validate CRM data. Automatically standardizes names, addresses, phone numbers, and LinkedIn URLs while updating records via Zoho CRM API to maintain clean and consistent data.

```
void automation.update2(Int id)
{
    // ================= GET RECORD =================
    rec = zoho.crm.getRecordById("Crm_to_Creator_test", id);

    Name1 = ifnull(rec.get("Name1"), "");
    Company_Name = ifnull(rec.get("Company_Name"), "");
    Phone = ifnull(rec.get("Phone"), "");
    Street = ifnull(rec.get("Street"), "");
    City = ifnull(rec.get("City"), "");
    State = ifnull(rec.get("State"), "");
    Country = ifnull(rec.get("Country"), "");

    updateMap = Map();

    // ================= NAME FORMAT =================
    Name1 = Name1.toLowerCase();
    parts = Name1.toList(" ");
    finalName = "";

    for each part in parts
    {
        if(part != "")
        {
            finalName = finalName + part.left(1).toUpperCase() + part.subString(1) + " ";
        }
    }
    updateMap.put("Name1", finalName.trim());

    // ================= COMPANY NAME FORMAT =================
    Company_Name = Company_Name.toLowerCase();
    parts = Company_Name.toList(" ");
    finalCompany = "";

    for each part in parts
    {
        if(part != "")
        {
            finalCompany = finalCompany + part.left(1).toUpperCase() + part.subString(1) + " ";
        }
    }
    updateMap.put("Company_Name", finalCompany.trim());

    // ================= PHONE FORMAT =================
    digits = Phone.replaceAll("[^0-9]", "");

    if(digits.length() == 11 || digits.startsWith("1"))
    {
        digits = digits.subString(1);
    }

    if(digits.length() == 10)
    {
        Phone = "+91-" + digits.subString(0,5) + "-" + digits.subString(5,10);
    }

    updateMap.put("Phone", Phone);

    // ================= STREET FORMAT =================
    Street = Street.toLowerCase();
    parts = Street.toList(" ");
    finalStreet = "";

    for each part in parts
    {
        if(part != "")
        {
            finalStreet = finalStreet + part.left(1).toUpperCase() + part.subString(1) + " ";
        }
    }
    updateMap.put("Street", finalStreet.trim());

    // ================= CITY FORMAT =================
    City = City.toLowerCase();
    parts = City.toList(" ");
    finalCity = "";

    for each part in parts
    {
        if(part != "")
        {
            finalCity = finalCity + part.left(1).toUpperCase() + part.subString(1) + " ";
        }
    }
    updateMap.put("City", finalCity.trim());

    // ================= STATE FORMAT =================
    State = State.toLowerCase();
    parts = State.toList(" ");
    finalState = "";

    for each part in parts
    {
        if(part != "")
        {
            finalState = finalState + part.left(1).toUpperCase() + part.subString(1) + " ";
        }
    }
    updateMap.put("State", finalState.trim());

    // ================= COUNTRY FORMAT =================
    Country = Country.toLowerCase();
    parts = Country.toList(" ");
    finalCountry = "";

    for each part in parts
    {
        if(part != "")
        {
            finalCountry = finalCountry + part.left(1).toUpperCase() + part.subString(1) + " ";
        }
    }
    updateMap.put("Country", finalCountry.trim());

    // ================= UPDATE RECORD =================
    resp = zoho.crm.updateRecord("Crm_to_Creator_test", id, updateMap);
    info resp;
}

```
