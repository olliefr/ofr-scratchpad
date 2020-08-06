# Network Time Protocol (NTP)

...

## What is a leap second?

> A *leap second* is a one-second adjustment that is occasionally applied to Coordinated Universal Time (UTC), to accommodate the difference between precise time (as measured by atomic clocks) and imprecise observed solar time (known as UT1 and which varies due to irregularities and long-term slowdown in the Earth's rotation). 
> 
> The UTC time standard, widely used for international timekeeping and as the reference for civil time in most countries, uses precise atomic time and consequently would run ahead of observed solar time unless it is reset to UT1 as needed. 
> 
> The leap second facility exists to provide this adjustment. 

Source: [Wikipedia](https://en.wikipedia.org/wiki/Leap_second)

## Leap second smearing

*Leap second smearing* is a technology used to adjust time in computers without adverse consequences.

No commonly used operating system is able to handle a minute with 61 seconds, and trying to special-case the leap second has caused [many problems](https://www.wired.com/2012/07/leap-second-glitch-explained/) in the past. Instead of adding a single extra second to the end of the day, one can run the clocks 0.0014% slower across the ten hours before and ten hours after the leap second, and "smear" the extra second across these twenty hours. For timekeeping purposes, December 31 will seem like any other day.

<hr>
> All Google services, including all APIs, will be synchronized on smeared time. 

Source: Google Cloud Platform [announcement](https://cloud.google.com/blog/products/gcp/making-every-leap-second-count-with-our-new-public-ntp-servers).
<hr>

[Google Public NTP](https://developers.google.com/time) serves *leap-smeared time* to smoothly handle leap seconds with no disruptive events.

This means the service is useful for anyone who would like to keep local clocks in sync with VM instances running on Google Compute Engine, to match the time used by Google APIs, or for those who just need a reliable time service.

&mdash; Oliver Frolovs, 2020