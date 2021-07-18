Sunrise Sunset
==============

This is a short C# file for calculating sunrise/sunset/twilight times (UTC), on a given day, at a given position.
This is the C# implementation of [Paul Schlyter's sunriset.c](http://stjarnhimlen.se/comp/sunriset.c).

Getting started
---------------

Get sunrise/sunset time and convert it to a string
````c#
double tsunrise, tsunset;
// Parameters : year - month - day - lat - long
Sunriset.SunriseSunset(2017, 2, 6, 46.214973, 5.241947, out tsunrise, out tsunset);
TimeSpan sunriseTime = TimeSpan.FromHours(tsunrise);
string sunriseTimeString = sunriseTime.ToString(@"hh\:mm\:ss");
Console.WriteLine(tsunrise+" "+sunriseTimeString);
```

Get civil/nautical/astronomical twilight times
````c#
double tsunrise, tsunset;
Sunriset.CivilTwilight(2017, 2, 6, 46.214973, 5.241947, out tsunrise, out tsunset);
Sunriset.NauticalTwilight(2017, 2, 6, 46.214973, 5.241947, out tsunrise, out tsunset);
Sunriset.AstronomicalTwilight(2017, 2, 6, 46.214973, 5.241947, out tsunrise, out tsunset);
```


https://www.codeproject.com/Articles/29306/C-Class-for-Calculating-Sunrise-and-Sunset-Times

C# Class for Calculating Sunrise and Sunset Times

Zacky Pickholz
Rate me:






4.25/5 (17 votes)
13 Sep 2008
Public Domain
1 min read
A class for calculating sunrise and sunset times, implemented as a thread-safe Singleton
Download source - 3.59 KB
Introduction
This simple C# Singleton class calculates the sunrise and sunset times for a given date.

Background
After searching for a simple and decent implementation for calculating sunrise and sunset times for given dates, and trying several implementations that were either too complicated to migrate to C# or simply not working, I found a simple yet working JavaScript implementation here.

I migrated the code to C#, tweaking it a little so that it provides accurate calculations. Also, I wrapped it as a Singleton class (assuming multiple instances would not be required for such a class) and added a lock to the main calculation method, in order to make it thread safe (via blocking).

Using the Code
The singleton class SunTimes can be called from anywhere in your code by calling SunTimes.Instance.

The class contains a single method, with one overload, named CalculateSunRiseSetTimes(). You simply call this method, provide it with three input parameters: latitude and longitude of the desired location, and date for which to calculate. Moreover, you need to pass it four (4) output (ref) parameters: riseTime (sunrise time), setTime (sunset time), isSunrise (does the sun rise that day at all?) and isSunset (does the sun set that day at all?).

The method returns a boolean value if the calculation succeeds (it will fail, if the time zone and longitude are incompatible).

Here is a sample usage of the class:

C#
Copy Code
...

DateTime date = DateTime.Today;
bool isSunrise = false;
bool isSunset = false;
DateTime sunrise = DateTime.Now;
DateTime sunset = DateTime.Now;

// Print out the Sunrise and Sunset times for the next 20 days
for (int i=0; i<20; i++)
{
                                                // Coordinates of Tel-Aviv
     SunTimes.Instance.CalculateSunRiseSetTimes(new SunTimes.LatitudeCoords
                                   (32, 4, 0, SunTimes.LatitudeCoords.Direction.North),
                                                new SunTimes.LongitudeCoords
                                   (34, 46, 0, SunTimes.LongitudeCoords.Direction.East),
                                                date, ref sunrise, ref sunset, 
			                     ref isSunrise, ref isSunset);

     Debug.Print(date + '': Sunrise @'' + sunrise.ToString('HH:mm') + ''  
				Sunset @'' + sunset.ToString(''HH:mm''));

     date = date.AddDays(1); // Move to the next day
}

...
Points of Interest
This implementation is not in particular fancy, not is it the slickest design, but hey - it does the work (at least as far as I've tested it). I will be happy to get any comments (not on its design, please, only if you detect any actual bugs).

History
14-Sep-2008: Uploaded the class implementation

License
This article, along with any associated source code and files, is licensed under A Public Domain dedication






https://github.com/bp2008/DahuaSunriseSunset

https://stackoverflow.com/questions/2056555/c-sharp-sunrise-sunset-with-latitude-longitude

NOAA Solar Calculator
https://gml.noaa.gov/grad/solcalc/
https://gml.noaa.gov/grad/solcalc/main.js


https://en.wikipedia.org/wiki/Sunrise_equation#Complete_calculation_on_Earth
https://en.wikipedia.org/wiki/Hour_angle

https://gml.noaa.gov/grad/solcalc/calcdetails.html

