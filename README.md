# Projectile Motion Lab Simulation

## Created to simulate the lab - code can run an experiment much faster than I can!

### It turns out, the results seem to be pretty close to what the results are in real life.

```python
from random import *
from math import *

# Horizontal Projectile Motion Lab Simulation Through Code - A comparison of results using code for my science lab
# Created 100% by Jaymin Ding!  Please do not use without his permission.
# I created this because code can run an experiment much faster than I can ;)
# This was created purely for fun and to compare results with my error analysis - it turns out that the error analysis was pretty accurate.
# I did the actual experiment, and I created this solely for comparison.

class HorizontalProjectileMotionLab:
    '''Represents a simulation of the horizontal projectile motion lab'''

    def __init__(self,distance,targetDistance,height,rollingTime,numTrials,gConstant=9.81):
        '''HorizontalProjectileMotionLab.(distance,height,rollingTime,gConstant=9.81) -> str
        Takes the inputs for the distance, height, rolling time, and the gravitational constant (which is by default set to 9.81 m/s^2)
        :param distance: The distance travelled (measured in real life)
        :type distance: float or int
        :param targetDistance: The distance the target is away from the table
        :type targetDistance: float or int
        :param height: The height of the table
        :type height: float or int
        :param rollingTime: The time it takes for the ball to roll to the edge
        :type rollingTime: float or int
        :param numTrials: The number of trials you want to run
        :type numTrials: int
        :param gConstant: The gravitational constant for the location
        :type gConstant: float or int'''
        self.distance = distance # meters (m)
        self.targetDistance = targetDistance # meters (m)
        self.height = height # meters (m)
        self.t_roll = rollingTime # seconds (s)
        self.v_x = self.distance/self.t_roll # meters per second (m/s)
        self.gConstant = gConstant # meters per second squared (m/s^2)
        self.t_fall = sqrt((2 * self.height) / self.gConstant) # seconds (s)
        self.horizontalDistance = self.v_x * self.t_fall # meters (m)
        self.goIn = 0 # if the ball stays in the box
        self.bounceOut = 0 # if the ball goes in, but then bounces out of the box
        self.goOut = 0 # if the ball completely misses the box, which won't happen based on the calculations I made (in my lab)
        self.numTrials = numTrials # number of trials

    def showResults(self):
        '''Horizontal.showResults(self) -> str
        :return: Whether or not the ball landed in the target based on the inputs given
        :rtype: str'''
        for _ in range(0,self.numTrials): # run the code however many trials we want
            self.errorConstant = randint(1,100) # redefine the small chance that we're going to make an error every single time, so it's completely random
            if self.errorConstant >= 80: # so based on my results, there was a 1/5 chance that the ball would actually stay in the box, so use that here
                if self.targetDistance - self.horizontalDistance == 0.1 or self.horizontalDistance - self.targetDistance == 0.1 or 0 < self.distance - self.horizontalDistance < 0.1 or 0 < self.horizontalDistance - self.targetDistance < 0.1: # make it so that there's a small margin of error
                    self.goIn += 1 # tally up the times that it went in
                    print('The ball went directly in the box and stayed in.')
                if 0.3 > self.targetDistance - self.horizontalDistance > 0.1 or 0.3 > self.horizontalDistance - self.targetDistance > 0.1: # another small margin of error, if it's in that range then it bounces out
                    self.bounceOut += 1 # tally up the times that it bounced out
                    print('The ball went into the box, but bounced out.')
                if self.targetDistance - self.horizontalDistance > 0.3 or self.horizontalDistance - self.targetDistance > 0.3: # if it's not within the margin of error at all
                    self.goOut += 1 # tally up the times that it completely missed
                    print('The ball did not go into the box.')
            if self.errorConstant < 80: # 4/5 probability of the ball definitely not going in - especially because humans are not perfect, and the ball is not going to roll in an exact straight line
                if 0 < self.targetDistance - self.horizontalDistance <= 0.1 or 0 < self.horizontalDistance - self.targetDistance <= 0.1:
                    self.bounceOut += 1
                    print('The ball went into the box, but bounced out.')
                if self.targetDistance - self.horizontalDistance > 0.1 or self.horizontalDistance - self.targetDistance > 0.1:
                    self.goOut += 1
                    print('The ball did not go into the box.')
        return "\nNumber of times the ball went in: " + str(self.goIn) + "\nNumber of times the ball went in, but bounced out: " + str(self.bounceOut) + "\nNumber of times the ball completely missed: " + str(self.goOut)

            

def simLab(distance,targetDistance,height,rollingTime,numTrials=5): # the number of trials by default is 5, which is the number of trials our lab has
    '''simLab(numTrials) -> ()
    runs the HorizontalProjectileLab'''
    print(HorizontalProjectileMotionLab(distance,targetDistance,height,rollingTime,numTrials).showResults())
simLab(0.41,0.39,0.75,0.35,1000)
# It turns out, that, the more trials I run, the closer the results seem to be that 1/5 of the time, the ball will stay inside the box, and 4/5 of the time, the ball will bounce out of the box.
```
