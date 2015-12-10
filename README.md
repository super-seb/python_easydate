# python_easydate
Datetime utility package for python 2.7 that makes datetime manipulation and time series generation very simple

> examples

	# create new easydate object
	ed = EasyDate()
	ed = EasyDate(local=False)
	ed = EasyDate(date_time='2015-03-09 09:16:43', local=True)
	ed = EasyDate(date_time=datetime(2015, 03, 9, 9, 16, 43), local=True)
	ed = EasyDate(date_time='now', local=True)
	
	# print reference point time in local or utc
	ed.return_string(format='datetime', local=True)
	ed.return_string(format='date', local=False)
	print ed.time_object_local
	print ed.time_object_utc
	
	# update or reset object
	ed.set_reference_point(date_time='2015-03-09 09:16:43', local=True)
	ed.set_reference_point(date_time=datetime(2015, 03, 9, 9, 16, 43), local=True)
	ed.set_reference_point(local=False)
	
	# get a date range
	print ed.get_range(period='day', n_periods=1, local=True)
	print ed.get_range(period='week', n_periods=1, local=True)
	print ed.get_range(period='month', n_periods=1, local=True)
	
	# move the reference point in increments
	ed.move_reference_point(period="day", n_periods=7)
	ed.move_reference_point(period="month", n_periods=-1)
	
	# move the reference point to the next weekday or month end
	ed.move_reference_to_next(next_time='friday', local=True)
	ed.move_reference_to_next(next_time='tuesday', local=True)
	ed.move_reference_to_next(next_time='month', local=True)
	ed.return_string(format='datetime', local=True)
	
	# generate a pandas data set of start/end times for a specified frequency, size and offset
	ed.generate_sequence(period='day', n_periods=14)
	ed.generate_sequence(period='week', n_periods=5)
	ed.generate_sequence(period='fortnight', n_periods=10)
	ed.generate_sequence(period='month', offset=0)
	ed.generate_sequence(period='month', offset=5)

