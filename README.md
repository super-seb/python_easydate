# python_easydate
Datetime utility package for python 2.7 that makes datetime manipulation and time series generation very simple

# Purpose and approach
This package was built to make some date and time manipulations very simple by wrapping key functionality into an easy to use object. In particular it is built: 
- to hold a reference time point that can then be moved forward or backward in easy to understand increments
- return time ranges (start/end datetimes) for any common range specified in plain english
- easily find the next day by its name, month end, quarter end, half year end or year end
- generate sequences of start/end datetimes for any common frequency specified in plain english
- easily convert UTC to a local timezone and account for cases that stradle days in calculations

# Example uses
> Creating new easydate objects

	# default initialises the reference time right now
	ed = EasyDate()

	# setting a local timezone, default is 'Australia/Brisbane'
	ed = EasyDate(local_timezone='Australia/Brisbane')

	# initialised with a datetime string which can be UTC or local time
	ed = EasyDate(date_time='2015-03-09 09:16:43', local=True)
	ed = EasyDate(date_time='2015-03-09 09:16:43', local=False)

	# initialised with a datetime object
	ed = EasyDate(date_time=datetime(2015, 03, 9, 9, 16, 43), local=True)

> Printing and returning date and datetime strings in local timezone or utc
	
	# return a date or datetime string of the reference time for UTC or local time
	ed.return_string(format='datetime', local=True)
	ed.return_string(format='date', local=False)

	# printing the internal variables that hold this data
	print ed.time_object_local
	print ed.time_object_utc

> Reseting the reference time point
	
	# reset the reference point with a datetime string being local or UTC time
	ed.set_reference_point(date_time='2015-03-09 09:16:43', local=True)

	# or a datetime object
	ed.set_reference_point(date_time=datetime(2015, 03, 9, 9, 16, 43), local=True)

	# or to the current time
	ed.set_reference_point(local=False)

> Returning a date range (start and end datetimes) for a given period
	
	# get a date range for 1 day for the local ot UTC time. Where UTC is on a different day to the local time (eg, 9.30am AEST is 11.30 UTC on the previous day) the range returned will be difference for local and UTC zones
	print ed.get_range(period='day', n_periods=1, local=True)
	
	# get the start and end of a 2 week period ending on the reference time day
	print ed.get_range(period='week', n_periods=2, local=True)
	
	# get the start and end of a 4 month period ending on the reference time day
	print ed.get_range(period='month', n_periods=4, local=True)
	
> Moving the reference point in increments

	# move the reference time forward 7 days
	ed.move_reference_point(period="day", n_periods=7)
	
	# move the reference time back 2 months
	ed.move_reference_point(period="month", n_periods=-2)

> Moving the reference point to the next weekday, month end, quarter end or year end
	
	# move the reference point to the next Friday local time. You can move to any weekday by specifying the name in lower case. This makes it easy to create custom date sequences ending on any day
	ed.move_reference_to_next(next_time='friday', local=True)
	
	# move to next Tuesday
	ed.move_reference_to_next(next_time='tuesday', local=True)

	# move to the next month end
	ed.move_reference_to_next(next_time='month', local=True)

> Generating date sequences for specificed frequencies as a pandas dataframe
	
	# return a 14 row sequence of days with the start and end datetime of each increment
	ed.generate_sequence(period='day', n_periods=14)

	# return a 5 week sequnce
	ed.generate_sequence(period='week', n_periods=5)

	# return a 10 row fortnightly (2 weeks) sequence
	ed.generate_sequence(period='fortnight', n_periods=10)

	# return a monthly sequence. Defaults to 30 rows
	ed.generate_sequence(period='month', offset=0)

	# return a monthly sequence offset by 5 months from the reference time (sequence ends 5 months after the reference time)
	ed.generate_sequence(period='month', offset=5)

