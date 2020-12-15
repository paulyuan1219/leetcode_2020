# Angle Between Hands of a Clock


Given two numbers, hour and minutes. Return the smaller angle (in degrees) formed between the hour and the minute hand.

Solution 1: Trivial

```
class Solution(object):
    def angleClock(self, hour, minutes):
        """
        :type hour: int
        :type minutes: int
        :rtype: float
        """
        
        angle_minutes = float(minutes) * 6 # a complete circle is 360 degrees, i.e. 6 degrees / minute
        angle_hour = (hour + float(minutes)/60) * 30 # a complete circle is 360 degrees, i.e. 30 degrees / hour
        
        if angle_hour > 360.0:
            angle_hour -= 360.0        
        
        res = abs(angle_hour - angle_minutes)
        
        return res if res < 180 else 360.0 - res
```