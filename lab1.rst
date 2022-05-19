Lab : Protecting AWS Hosted Web Application with F5 Distributed Cloud BotDefense
================================================================================

The purpose of this lab is to leverage F5 Distributed Cloud BotDefense to further
secure an AWS hosted Web application from advanced AI-driven Bot attacks.  
Lab attendees lab will utilize the F5 Distribted Cloud Platform and Global Network
to engage both signature-based Bot protections and then extend those protections 
with AI-enhanced Bot migitation strategies with BotDefense. Attendees will configure
and test BotDefense along with exploring the F5 Distributed Cloud Console and its 
features.

Objective:
----------

-  Gain an understanding of F5 Distributed Cloud BotDefense, its configuration and
   implmentation.

-  Gain an initial understanding of the F5 Distributed Cloud Platform and Console in
   in further securing AWS hosted applications and services.

Lab Requirements:
-----------------

-  All Lab requirements will be noted in the tasks that follow

-  Estimated completion time: 15 minutes

Lab Tasks:
-----------------

TASK 1: F5 Distributed Cloud Console Login.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following will guide you through the initial Lab environment access within the 
F5 Distributed Cloud Console.  You should have received an email with an invitation to 
access F5 Distributed Cloud Console.

The name of the F5 Distributed Cloud tenant that we will be using is **f5-sales-public**

You will need to create a password that will be associated with your email address. If you
have NOT received an email from our system you may need to provide an alternate email address
that we can use for the purposes of this lab.

F5 Dsitributed Cloud Console is a SaaS control-plane for services that provides a UI and API
for managing network, security, and compute services. F5 Distributed Cloud Console can manage
"sites" in existing on-prem data centers and sites in AWS, Azure, and GCP cloud environments.

+----------------------------------------------------------------------------------------------+
| 1. Please log into your assigned Volterra tenant.                                            |
|    https://f5-sales-public.console.ves.volterra.io/                                          |
|                                                                                              |
| 2. When you first login you will need to select your "persona"                               |
|                                                                                              |
| 3. Enter your persona as "SecOps" and level as "Intermediate". You can change these settings |
|    after logging in as well.                                                                 |
|                                                                                              |
| 4. Several "Guidance ToolTips" will appear, you can safely close these out.                  |
|                                                                                              |
| 5. You can identify your namespace (an environment for isolating configured applications) by |
|    clicking on **Account Settings** and expanding the **Account** icon in the top right of   |
|    the screen and clicking on **Account Settings**                                           |
|                                                                                              |
| 5. Next click on "My Namespaces" and take note of the studentxxx namespace that you have been|
|    assigned. Each student will have a unique number.                                         |
+----------------------------------------------------------------------------------------------+
| |image00a|                                                                                   |
| |image00b|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 2: Build an Load Balancer with associated secuirty confingurations.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following steps will allow you to deploy and advertise a globally available and
secured application.  These steps will define an application, register its DNS, and
target an origin (AWS hosted application) in prepartion of attaching Bot Protection
Strategies.

+----------------------------------------------------------------------------------------------+
| 1. Ensure you are in your studentxxx namespace                                               |
|                                                                                              |
| 2. In the left Navigation expand **Manage** and click "Load Balancers > HTTP Load Balancers" |
|                                                                                              |
| 3. Click the **Add HTTP Load Balancer** in the graphic as shown.                             |
+----------------------------------------------------------------------------------------------+
| |image001|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 4. Using the left navigation and in the sections as presented, enter the following data.     |
|    Values where **xxx** is required, use the student number associated with your namespace.  |
|                                                                                              |
|    **Metdata:Name ID:**  **studentxxx-lb**                                                   |
|                                                                                              |
|    **Basic Configuration:List of Domains:** **studentxxx.sales-public.f5demos.com**          |
|    **Basic Configuration:Select Type of Load Balancer:** **HTTP**                            |
|    **Basic Configuration:Automatically Manage DNS Records** Check the Box                    |
+----------------------------------------------------------------------------------------------+
| |image002|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 5. In the current window left navigation,  click **Default Origin Servers** and then         |
|                                                                                              |
|    **Add Item**.                                                                             |
|                                                                                              |
| 6. In the resulting window, use the drop down as shown and click **Create new Origin Pool**. |
+----------------------------------------------------------------------------------------------+
| |image003|                                                                                   |
|                                                                                              |
| |image004|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 8. In the resulting window, **enter studentxxx-pool** and click **Add Item** under **Basic** |
|                                                                                              |
|    **Configuration: Origin Servers**                                                         |
|                                                                                              |
| 9. ** Pulic DNS Name of Origin Server** should be selected.  For **DNS Name** enter the      |
|                                                                                              |
|    following hostanme **demo-app.cloud.myf5demo.com** and click **Add Item**                 |
+----------------------------------------------------------------------------------------------+
| |image005|                                                                                   |
|                                                                                              |
| |image006|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 10. After returning to the prior window, make sure **Port:** in configured for **80**.       |
|                                                                                              |
| 11. Leave all other values as default while scrolling to the bottom an click, **Continue**.  |
|                                                                                              |
| 12. After returning to the next windo and confirming the content, click **Add Item**.        |
+----------------------------------------------------------------------------------------------+
| |image007|                                                                                   |
|                                                                                              |
| |image008|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 13. In the left hand navigation of the main window, click **Security Configuration**.        |
|                                                                                              |
| 14. Use the drop down for **Select Web Application Firewall (WAF Config)** and select        |
|                                                                                              |
|     **App Firewall**.                                                                        |
|                                                                                              |
| 15. In the resulting **App Firewall** drop down select **Create new App Firewall**.          |
+----------------------------------------------------------------------------------------------+
| |image009|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 16. In the resulting window Metadata section enter **studentxxx-appfw** for the **Name**.    |
|                                                                                              |
| 17. Under **Enforcement Mode**, chnage the Enforcement Mode to **Blocking**.                 |
|                                                                                              |
| 18. Leaving all other values as default, scroll to the bottom and click **Continue**.        |
|                                                                                              |
| 19. Leaving all other values as default, scroll to the bottom and click **Save and Exit**.   |
+----------------------------------------------------------------------------------------------+
| |image011|                                                                                   |
|                                                                                              |
| |image012|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 19. In the resulting window, scroll to the bottom and click **Save and Exit**.               |
|                                                                                              |
| 20. In the final window note application hostname under the **Domains** column (Step 4).     |
+----------------------------------------------------------------------------------------------+
| |image013|                                                                                   |
+----------------------------------------------------------------------------------------------+


TASK 3: Testing Application then Adding BotDefense  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Now that the application has been confgured and is accessible, we can attach BotDefense and see
the "before" and "after" affects.

+----------------------------------------------------------------------------------------------+
| 1. Open another tab in your browser, enable developer tools (Firefox shown (use F12)) and    |
|    click on the **Network** tab.                                                             |
|                                                                                              |
| 2. In browser's main URL window, navigate to **http://studentxxx.sales-public.f5demo.com**   |
|                                                                                              |
| 3. Using the 3 bars/menu icon (top right), navigate to **Access** link.                      |
|                                                                                              |
| 3. In the resulting login screen use the following values to login                           |
|    **Identity:** **user@f5.com**                                                             |
| 3. Using the 3 bars/menu icon (top right), navigate to **Access** link.                      |
+----------------------------------------------------------------------------------------------+
| |image014|                                                                                   |
+----------------------------------------------------------------------------------------------+

.. |image00a| image:: media/account-settings.png
   :width: 800px
.. |image00b| image:: media/mynamespaces.png
   :width: 800px
.. |image001| image:: media/lb-001.png
   :width: 800px
.. |image002| image:: media/lb-002.png
   :width: 800px
.. |image003| image:: media/lb-003.png
   :width: 800px
.. |image004| image:: media/lb-004.png
   :width: 800px
.. |image005| image:: media/lb-005.png
   :width: 800px
.. |image006| image:: media/lb-006.png
   :width: 800px
.. |image007| image:: media/lb-007.png
   :width: 800px
.. |image008| image:: media/lb-008.png
   :width: 800px
.. |image009| image:: media/lb-009.png
   :width: 800px
.. |image010| image:: media/lb-010.png
   :width: 800px
.. |image011| image:: media/lb-011.png
   :width: 800px
.. |image012| image:: media/lb-012.png
   :width: 800px
.. |image013| image:: media/lb-013.png
   :width: 800px
.. |image014| image:: media/lb-014.png
   :width: 800px
.. |image015| image:: media/lb-015.png
   :width: 800px
.. |image016| image:: media/lb-016.png
   :width: 800px
.. |image017| image:: media/lb-017.png
   :width: 800px
.. |image018| image:: media/lab1-018.png
   :width: 800px
.. |image019| image:: media/lab1-019.png
   :width: 800px
.. |image020| image:: media/lab1-020.png
   :width: 800px
.. |image021| image:: media/lab1-021.png
   :width: 800px
.. |image022| image:: media/lab1-022.png
   :width: 800px
.. |image023| image:: media/lab1-023.png
   :width: 800px
.. |image024| image:: media/lab1-024.png
   :width: 800px
.. |image025| image:: media/lab1-025.png
   :width: 800px
.. |image026| image:: media/lab1-026.png
   :width: 800px
.. |image027| image:: media/lab1-027.png
   :width: 800px
.. |image028| image:: media/lab1-028.png
   :width: 800px
.. |image029| image:: media/lab1-029.png
   :width: 800px
.. |image030| image:: media/lab1-030.png
   :width: 800px
.. |image031| image:: media/lab1-031.png
   :width: 800px
.. |image032| image:: media/lab1-032.png
   :width: 800px
.. |image033| image:: media/lab1-033.png
   :width: 800px
.. |image034| image:: media/lab1-034.png
   :width: 800px
.. |image035| image:: media/lab1-035.png
   :width: 800px
.. |image036| image:: media/lab1-036.png
   :width: 800px
.. |image037| image:: media/lab1-037.png
   :width: 800px
.. |image038| image:: media/lab1-038.png
   :width: 800px
.. |image039| image:: media/lab1-039.png
   :width: 800px
.. |image040| image:: media/lab1-040.png
   :width: 800px
.. |image041| image:: media/lab1-041.png
   :width: 800px
.. |image042| image:: media/lab1-042.png
   :width: 800px
.. |image043| image:: media/lab1-043.png
   :width: 800px
.. |image044| image:: media/lab1-044.png
   :width: 800px
.. |image045| image:: media/lab1-045.png
   :width: 800px
      
