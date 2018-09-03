## Writeup

---

**PID Control Project**

The goals / steps of this project are the following:
* Implement PID controller in C++.
* Tune PID gains to go around the lake in project simulator as fast as possible.
* Write how I tune PID gains.

#### [Rubric](https://review.udacity.com/#!/rubrics/824/view)

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.

---

### Discussion

#### 1. Here I briefly discuss how each gain affect the motion of the car in simulation.

The function of P gain is to reduce the cross track error(CTE), that means it makes the car's center position be on the target track. The more the P gain is, the faster it reduce the CTE, however the overshoot and the residual error get larger. Also, it cannot make the direction difference be reduced, therefore it has never be converged. Here is the [video that only uses P gain](./videos/P_only.mp4). As you can see, it cannot turn well.
Second, the function of D gain(includes dividing by time difference) is to reduce the direction difference. That is, it penalizes the difference of car's heading and the target track's slope. So, owing to D gain, the car's heading can be parallel to the target track. For example, if the car start turning, D gain works well because the direction difference gets larger in that position. Also, D gain reduces overshoot.
Third, I gain reduce residual error. In order the car to curve well, D gain effect should be large comparing to that of P gain. So the Car moves so that its direction gets parallel to the target track's slope, but CTE reduces slowly.
Thus, I gain reduces such residuals. I had to be careful because if I gain is too large, it easily became unstable and it oscillates soon.



#### 2. 1. Here I briefly discuss how I tune each gain.

This is the final parameters I have tuned.

| Parameters    | Values    |
|:-------------:|:-------------:|
| P gain        |  0.2      |
| I gain        |  0.0002   |
| D gain        |  9.0      |
| Target speed  |  35.0     |

Here is a link to [my video result](./videos/PID_final.mp4). The speed of the video is 4 times faster than real one.

I manually tune my parameters. I print all the control values(the gain multiplies by the error). First, I tune P gain so that it tracks the target track well and the car's oscillation does not happen. Next, I tuned D parameter so the car can turn curves well.  Finally I tune I gain so that the CTE gets lower. Always, I used the information of each control value. If the difference between each gain is too large it could not work well.

#### 3. Here I briefly discuss how I improve my program.

There is one way to improve my program. I can change speed using the information of the CTE. If the CTE is large, it can be on the curve, so I can reduce speed and car could turn well. On the other hand, if the CTE is small, it must be on straight track, so the car's speed could be larger.
