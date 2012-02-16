# arrrrug_2012_02

!SLIDE

# relativity
# EntityMap

## @peter_v

!SLIDE

# "6 o'clock"
# "7 to 5"
### (El Fish - Copydog)

```ruby
Time.new # => 2012-02-15 21:56:51 0100

require 'date'
Date.new # => #<Date: -4712-01-01 ((0j,0s,0n),+0s,2299161j)>

DateTime.new # => #<DateTime: -4712-01-01T00:00:00+00:00 ((0j,0s,0n),+0s,2299161j)>

"7 to 5" # => "7 to 5" ??
```
!SLIDE

# relativity

```ruby
require 'relativity'
start_at = DayTime.new("6") # => 06:00:00
end_at = DayTime.new("12:35:30") # => 12:35:30
now = DayTime.new # => 22:09:42

seven_to_five = DayTimeRange.new("7 to 17")
# => 07:00:00 to 17:00:00
night_shift = DayTimeRange.new("21:55 until 6:55:30")
# => 21:55:00 until 06:55:30
```
!SLIDE

# persisting
### (to a string column)
```ruby
  class Shop < ActiveRecord::Base

    def opening_hours=(dtr)
      super(
        begin
          DayTimeRange.normalize(dtr, separator => '..')
        rescue Relativity::FormatError
          nil # or set a special error code here
        end)
      end
    end

    def opening_hours
      dtr = super and DayTimeRange.new(dtr, :separator => '..')
    end

  end
```

!SLIDE

# API / XML
```xml
<shop>
  <opening_hours type="DayTimeRange">09:00:00..12:30:00</opening_hours>
</shop>
```
!SLIDE

# API / JSON

shows the internal datastructure (a TODO)

```json
{"opening_hours":{"separator":"..",
"start_day_time":{"seconds_since_midnight":"32400.0"},
"end_day_time":{"seconds_since_midnight":"45000.0"}}}
```

!SLIDE

# TODO

```ruby
am = DayTimeRange.new("0...12")

WeekDay.new("Monday")
WeekTime.new("Monday 13:00")

weekend = WeekDayRange.new("Saturday to Sunday")
monday_open = WeekTimeRange.new(
  "Monday 13:00 to Monday 18:00")

publish_results = QuarterDay.new("20d")
payday = MonthDay("-3d")

if weekend.include?(Time.now)
 go_party
end

if pay_day.today?
  prepare_paycheck
end
```
