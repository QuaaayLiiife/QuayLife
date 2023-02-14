# Release Notes: September 2022

Customers can now generate snapshots for multi-service views they have configured. For more information on multi-service views, see

[Multi-Service Views](https://docs.thousandeyes.com/product-documentation/internet-and-wan-monitoring/tests/multi-service-views)

.

#### BrowserBot and Recorder IDE Upgrade to Chrome 97 Complete <a href="#browserbot-and-recorder-ide-upgrade-to-chrome-97-complete" id="browserbot-and-recorder-ide-upgrade-to-chrome-97-complete"></a>

The Recorder IDE and all Cloud and Enterprise Agents with auto-updates have been upgraded to use Chromium 97 with BrowserBot (v2.6.0+) and Recorder IDE v1.4.0.

Between Chromium v80 (BrowserBot v2.5.9 and prior) and Chromium v97, notable differences include:

* Recorder IDE stability on macOS devices.
* After an iframe is destroyed, Selenium WebDriver will no longer switch to the default content automatically.
* HTML elements with an area of zero are no longer clickable.
* shadowRoot no longer returns a WebElement.
* ChromeDriver does not wait for the HTML document to be loaded completely.

The upgrade to the NPCAP library on the Endpoint Agent client for Windows will now be done on September 28, 2022, and not on September 17, 2022, as communicated

[previously](https://docs.thousandeyes.com/whats-new/changelog#endpoint-agent-npcap-library-upgrade-to-version-1.55)

.

The ThousandEyes Support chat has been replaced by the new chatbot service, TEACH (ThousandEyes Assistant, Concierge, & Helper). For more information about TEACH, see

[Live Chat](https://docs.thousandeyes.com/product-documentation/getting-started/getting-support-from-thousandeyes#live-chat)

.

New Cloud Agents have been added to the following locations:

* Bangalore, India (Bharti Airtel)
* Bangalore, India (Bharti Airtel) (IPv6)
* Bangalore, India (Vodafone Idea)
* Bangalore, India (Vodafone Idea) (IPv6)
* Chennai, India (Vodafone Idea)
* Chennai, India (Vodafone Idea) (IPv6)
* Mumbai, India (Bharti Airtel)
* Mumbai, India (Bharti Airtel) (IPV6)
* Northampton, England (IPv6)
* An issue that caused edited dashboards to not save correctly after a refresh has been resolved.
* An issue that prevented refresh tokens from being generated for oAuth client credential authentication in custom webhooks has been fixed.
* An issue has been resolved where the filter options were not populating correctly on our live status widgets for dashboards.
* An issue that was causing reports in Japanese that were downloaded in PDF to be formatted incorrectly has been resolved.
* An issue was found where several group by options for our Endpoint Agent report and dashboard widgets were not available. This has now been corrected. The list of missing group bys were as follows:
* An issue that was incorrectly triggering dynamic baseline alerts that had multiple dynamic alert conditions attached to it, whether in the same rule or in multiple different rules, has been resolved.
* An issue was identified where timestamps for individual schedule HTTP server tests in the Endpoint Agent were not taking into account the user's timezone. This has been resolved, and you will now see the correct timestamps associated to each test taking into account the specific timezone.

New Cloud Agents have been added to the following locations:

* Cleveland, OH, USA (IPv6)
* Cleveland, OH, USA (Charter)
* Cleveland, OH, USA (Charter) (IPv6)
* Surabaya, Indonesia (IPv6)

**New Amazon Local Zone Cloud Agents**

* Boston, MA, USA (AWS Local Zone) (AWS us-east-1-bos-1)
* Chicago, IL, USA (AWS Local Zone) (AWS us-east-1-chi-1)
* Dallas, TX, USA (AWS Local Zone) (AWS us-east-1-dfw-1)
* Denver, CO, USA (AWS Local Zone) (AWS us-west-2-den-1)
* Houston, TX, USA (AWS Local Zone) (AWS us-east-1-iah-1)
* Kansas City, MO, USA (AWS Local Zone) (AWS us-east-1-mci-1)
* Las Vegas, NV, USA (AWS Local Zone) (AWS us-west-2-las-1)
* Los Angeles, CA, USA (AWS Local Zone) (AWS us-west-2-lax-1)
* Miami, FL, USA (AWS Local Zone) (AWS us-east-1-mia-1)
* Minneapolis, MN, USA (AWS Local Zone) (AWS us-east-1-msp-1)
* New York, NY, USA (AWS Local Zone) (AWS us-east-1-nyc-1)
* Philadelphia, PA, USA (AWS Local Zone) (AWS us-east-1-phl-1)
* Phoenix, AZ, USA (AWS Local Zone) (AWS us-west-2-pdx-1)
* An issue was fixed in the **Update Tests** API that prevented updating the port in Agent to Server tests if the server wasn't also specified.
* An issue was resolved that was preventing some dashboards from automatically updating every two minutes.
