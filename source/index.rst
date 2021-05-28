.. SafeNet Trusted Access documentation master file, created by
   sphinx-quickstart on Wed Mar 24 16:12:19 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

========================================================================
FortiGate VPN and FortiClient with SafeNet Trusted Access using SAML 2.0
========================================================================

.. toctree::
   :maxdepth: 3
   :hidden:

   index


Overview
========

This guide shows how to implement adaptive authentication with strong contextual security policies to FortiGate SSL VPN and the FortiClient using SAML federation with SafeNet Trusted Access


Prerequisites
=============

  - FortiOS 6.4.4.1803 and above
  - FortiClient 6.4.2.1580 and above
  - A user with a SafeNet Trusted Access authenticator enrolled
  - Users can authenticate using SafeNet Trusted Access

Configuration Overview
======================

The configuration requires the following steps:

  **In SafeNet Trusted Access**

  - `Create FortiGate Application in SafeNet Trusted Access`_
  - `Configure STA Authentication Policy`_

  **In FortGate**

  - `Add a SAML Identity Provider to FortiGate`_
  - `FortiClient VPN Configuration`_


SafeNet Trusted Access Configuration
====================================

_`Create FortiGate Application in SafeNet Trusted Access`
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

In the STA Console, add FortiGate application by following these steps:


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
