.. SafeNet Trusted Access documentation master file, created by
   sphinx-quickstart on Wed Mar 24 16:12:19 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

========================================================================================
Cisco ASA SSL VPN and Cisco AnyConnect Client with SafeNet Trusted Access using SAML 2.0
========================================================================================

.. toctree::
   :maxdepth: 3
   :hidden:

   index


Overview
========

This guide shows how to implement adaptive authentication with strong contextual security policies to Cisco ASA SSL VPN and Cisco AnyConnect Client using SAML federation with SafeNet Trusted Access


Prerequisites
=============

  - Cisco ASA 9.7.1.24 and above
  - Cisco AnyConnect 4.6 and above
  - A user with a SafeNet Trusted Access authenticator enrolled
  - Users can authenticate using SafeNet Trusted Access

Configuration Overview
======================

The configuration requires the following steps:

  **In SafeNet Trusted Access**

  - `Create Cisco ASA Application in SafeNet Trusted Access`_
  - `Configure STA Authentication Policy`_

  **In Cisco ASA**

  - `Add a SAML Identity Provider to Cisco ASA`_
  - `Cisco AnyConnect VPN Configuration`_


SafeNet Trusted Access Configuration
====================================

_`Create Cisco ASA Application in SafeNet Trusted Access`
*********************************************************

.. note:: Open SafeNet Trusted Access Console (you can use the following direct links based on your availability zone, opens in a new tab)

          |US Zone|

            .. |US Zone| raw:: html

              <a href="https://sta.us.safenetid.com" target="_blank">US Zone SafeNet Trusted Access Console</a>

          |EU Zone|

            .. |EU Zone| raw:: html

              <a href="https://sta.eu.safenetid.com" target="_blank">EU Zone SafeNet Trusted Access Console</a>

          |Classic Zone|

            .. |Classic Zone| raw:: html

              <a href="https://sta.safenetid.com" target="_blank">Classic Zone SafeNet Trusted Access Console</a>

In the STA Console, add Cisco ASA application by following these steps:

1. In **Applications** tab, click on the :guilabel:`+` button and search for **Generic Template**

.. thumbnail:: _images/applications.png

2. Name the application and choose **SAML** for the **Integration Protocol**

.. thumbnail:: _images/application.png

3. *Optional* - Change the Application Logo by clicking on the default icon. You can download Cisco ASA logo icon :download:`here <_downloads/asa-logo.png>`

.. thumbnail:: _images/add_icon.png

.. thumbnail:: _images/icon.png

  - Browse for or drag the logo icon downloaded above and click :guilabel:`Select`

4. Clcik :guilabel:`Add` to add the Cisco ASA Application

5. Switch to **Manual Configuration**

.. thumbnail:: _images/manual.png

.. _Cert:

- Download STA Tenant Certificate by clicking :guilabel:`Download X.509 certificate`

.. thumbnail:: _images/certificate.png

.. _SAML:

- Note both STA Tenant **Issuer/Entity ID** and STA **Single Sign-On Service** URL

.. thumbnail:: _images/entity.png

6. Click :guilabel:`Next Step`

.. note:: For the next step, leave the STA Application configuration and login to Cisco ASA using ASDM to configure SAML settings that will generate the Metadata file to be imported into the STA Cisco ASA Application to complete the STA Cisco ASA Application configuration


Cisco ASA Configuration
=======================

Import STA Certificate into Cisco ASA
*************************************

1. Login to **Cisco ASDM**

2. Click on :guilabel:`Configuration`

.. thumbnail:: _images/asdm_configuration.png

3. Click on :guilabel:`Remote Access VPN`

.. thumbnail:: _images/asdm_vpn.png

4. Expand :guilabel:`Certificate Management`

.. note:: The **CA Certificates** section is where the STA certificate will be imported to. The **Identity Certificates** section is where the Cisco ASA IDP certificate will be created

.. thumbnail:: _images/asdm_certs.png

5. Click on :guilabel:`CA Certificates` and click on :guilabel:`Add`

.. thumbnail:: _images/asdm_add_cert.png

6. Enter a **Trustpoint Name** for the STA certificate and browse to the certificate file that was downloaded in :ref:`in this step <Cert>`

.. thumbnail:: _images/asdm_trustpoint.png


_`Configure STA Authentication Policy`
**************************************

In the STA Console, create a new Access Policy for FortiGate application by following these steps:

  #. Go to the :guilabel:`Policies` tab

  #. Click :guilabel:`+` to add a new Policy

  #. Name the new Policy, *for example FortiGate VPN*

  - **Polcy Scope**

    #. Under **Users**, click :guilabel:`All Users` to apply to all users or :guilabel:`Any of these User Groups:` to apply to specifc User Groups

    #. Under **Applications**, click :guilabel:`Any of these Applications`, click in the field and select **FortiGate** application

  - **Default Requirements**

    #. Select the desired authentication method *for example* :guilabel:`Password` and :guilabel:`Every access attempt` and :guilabel:`Token Based Authentication (OTP)` and :guilabel:`Every access attempt`

  4. Click :guilabel:`Save` to save the new Policy


The SafeNet Trusted Access configuration of the FortiGate application is complete

FortiGate Configuration
=======================


Using FortiClient
*****************



Using SafeNet Trusted Access User Portal
****************************************
