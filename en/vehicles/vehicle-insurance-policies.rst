List of the vehicle insurance policies
######################################

Description of XML schema
=========================
A request is formed through URL (using GET method).

XSD-schema :

-  ``www/xsd/VehicleInsurancePoliciesResponse.xsd``

Request
-------

Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/vehicle_insurance_policies``

Response, VehicleInsurancePoliciesResponse
------------------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <VehicleInsurancePolicies>
            <VehicleInsurancePolicy 
                    id="..." 
                    name_ru="..." 
                    description_ru="..."
                    description_en="..."                 
            >...</VehicleInsurancePolicy> - insurance policy
        </VehicleInsurancePolicies>
    </Response>

Response Item/h3>
-----------------

Parent item.

**Attributes:** no.

**Child items:**

+--------------------------+-----------+----------------------------------------+
| Name                     | Mandatory | Description                            |
+==========================+===========+========================================+
| VehicleInsurancePolicies | Yes       | List of the vehicle insurance policies |
+--------------------------+-----------+----------------------------------------+

VehicleInsurancePolicies Item
-----------------------------

List of the insurance policies.

**Attributes:** No.

**Child items:**

+------------------------+-----------+--------------------------+
| Name                   | Mandatory | Description              |
+========================+===========+==========================+
| VehicleInsurancePolicy | No        | Vehicle insurance policy |
+------------------------+-----------+--------------------------+

VehicleInsurancePolicy Item
---------------------------

Insurance policy.

- Not Mandatory element

**Attributes:**

+----------------+---------+-----------+-------------------------------------------------+
| Name           | Type    | Mandatory | Description                                     |
+================+=========+===========+=================================================+
| id             | numeric | Yes       | id of the insurance policy                      |
+----------------+---------+-----------+-------------------------------------------------+
| name\_ru       | string  | Yes       | russian name of the insurance policy.           |
+----------------+---------+-----------+-------------------------------------------------+
| desciprion\_ru | string  | Yes       | Description (russian) of the insurance policy . |
+----------------+---------+-----------+-------------------------------------------------+
| desciprion\_en | string  | Yes       | Description (english) of the insurance policy.  |
+----------------+---------+-----------+-------------------------------------------------+

**Child items:** No.
