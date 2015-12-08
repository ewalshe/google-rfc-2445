# Google Code RFC-2445

## History

This was written by Mike Samuel and was available on the, now defunct, [Google Code](https://code.google.com/p/google-rfc-2445/)

## Using

Using the API is pretty easy.   Pass in some ical and you get back
a date iterable, which can be used in a for-each loop thusly:

    // A compatibility layer for joda-time
    import com.google.ical.compat.jodatime.LocalDateIteratorFactory;
    // A Joda time class that represents a day regardless of timezone
    import org.joda.time.LocalDate;

    public class ThirteenFridaysTheThirteenth {

      /** print the first 13 Friday the 13ths in the 3rd millenium AD. */
      public static void main(String[] args) throws java.text.ParseException {
	LocalDate start = new LocalDate(2001, 4, 13);

	// Every friday the thirteenth.
	String ical = "RRULE:FREQ=MONTHLY"
		      + ";BYDAY=FR"  // every Friday
		      + ";BYMONTHDAY=13"  // that occurs on the 13th of the month
		      + ";COUNT=13";  // stop after 13 occurences

	// Print out each date in the series.
	for (LocalDate date :
	     LocalDateIteratorFactory.createLocalDateIterable(ical, start, true)) {
	  System.out.println(date);
	}
      }

    }
    
See [RFC 2445](rfc2445.html#4.3.10) for the recurrence rule syntax and what it means, 
and the examples [later](rfc2445.html#4.8.5.4) in the same document.

If you use <code>java.util.Date</code> and <code>java.util.Calendar</code> in
your application instead of Joda-Time, you can use the
<code>com.google.ical.compat.javautil</code> package instead to provide
Date objects.

