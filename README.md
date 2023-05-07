Download Link: https://assignmentchef.com/product/solved-me227-assignment-6-linearization-and-project-reflection
<br>
For this homework, we will study linearization, reflect on the project, and start thinking about racing.

<h1>Instructions</h1>

This homework assignment will be submitted using Gradescope.

All written portions must be turned in through Gradescope. See the Piazza post on homework guidelines for more instructions on the different homework resources available to you. Whatever format you decide to use, please <strong>BOX </strong>all of your final answers.

1

<h1>Problem 1 – Linearization</h1>

In the last homework, you used your intuition about vehicle dynamics to determine signs of feedback gains to stabilize around a drift equilibrium. This week, we are going to learn how we can compute a linearization and use linear control techniques to determine these gains, rather than by inspection.

For all the following problems, consider a drift equilibrium consisting of <em>r<sub>eq </sub></em>= 0<em>.</em>7486 rad/s, <em>U<sub>y,eq </sub></em>= −8<em>.</em>661 m/s, <em>U<sub>x,eq </sub></em>= 10<em>.</em>3224 m/s, <em>δ<sub>eq </sub></em>= −0<em>.</em>5132 rad, and <em>F<sub>xr,eq </sub></em>= 7317 N.

(This is derived from drifting an 18 meter radius path (<em>κ </em>= 1<em>/</em>18) with constant sideslip of −40°)

<h2>Question 1.A – Linearization of our Velocity Dynamics (MATLAB Grader)</h2>

Up until now, we have linearized our dynamics via linear <em>assumptions</em>, such as small angle approximations and linear tires. We will now directly linearize our dynamics (which allows analysis and control of cool vehicle behavior such as drifting).

Consider just our velocity states, so <em>x </em>= [<em>r,U<sub>y</sub></em>]<em><sup>T</sup></em>. We can write our dynamics as being a nonlinear function of our state and steering input (forget <em>F<sub>xr </sub></em>for now – assume we are using the same longitudinal controller from HW5): <em>x</em>˙ = <em>f</em>(<em>x,δ</em>)

We can linearize the dynamics and write our system as:

<em>x</em>˙ = <em>f</em>(<em>x<sub>eq</sub></em>) + <em>A</em>(<em>x </em>− <em>x<sub>eq</sub></em>) + <em>B</em>(<em>δ </em>− <em>δ<sub>eq</sub></em>) = <em>A</em>(<em>x </em>− <em>x<sub>eq</sub></em>) + <em>B</em>(<em>δ </em>− <em>δ<sub>eq</sub></em>)

<em>x</em>¯˙ = <em>Ax</em>¯ + <em>Bδ</em><sup>¯</sup>

(6.1)

(6.2)

To calculate the partial derivatives, we need to carefully consider what each term in our dynamics is a function of. Based on the Fiala lateral tire model:

<em>F<sub>yf </sub></em>= <em>f</em>(<em>α<sub>f</sub></em>) = <em>f</em>(<em>U<sub>y</sub>,r,δ</em>)

Generally while drifting, <em>α<sub>r </sub>&gt; α<sub>sl </sub></em>so:

<em>F</em><em>yr </em>= <em>f</em>(<em>F</em><em>xr</em>)

So to calculate the first entry in the A matrix:

To calculate , we then need to take the derivative of each term in the Fiala model with respect to <em>r</em>. The rest of the derivatives can be computed similarly.

For this two state model we have computed the A &amp; B matrices for you (so you won’t need to take the derivative of the Fiala model). However, make sure you understand how one could compute each term in A &amp; B, as you will be finding some of the derivatives in the next problem.

(6.3)

(6.4)

Finally, lets use the control law <em>δ</em><sup>¯ </sup>= −<em>Kx</em>¯ (full state feedback).

<strong>Find the gain vector K that puts the poles of the closed loop system at -4 and -8. Compute this by hand and show your work. Submit your gain vector to MATLAB Grader.</strong>

<h2>Question 1.B – Incorporating Path Tracking (MATLAB Grader)</h2>

Drifting by itself is pretty cool, but what if we wanted to incorporate a reference path? Let’s define a new state <em>x </em>= [<em>r,U<sub>y</sub>,e,</em>∆<em>ψ</em>]<em><sup>T</sup></em>.

<strong>Find a value for </strong>∆<em>ψ<sub>eq </sub></em><strong>given the drift equilibrium we are using in this problem. Do not make any small angle assumptions.</strong>

Let’s linearize these dynamics as before and then try to find gains that stabilize the system. This time, our linearized matrices are:

(6.5)

(6.6)

<strong>Find </strong>∆<em>ψ<sub>ss </sub></em><strong>and the new linearized dynamics matrices. Using full state feedback as before, place the poles at [-4 +/- 4.5j, -0.15 +/- 0.75j]. You are encouraged to use the ’place’ function in</strong>

<strong>MATLAB. Report your gain vector and </strong>∆<em>ψ<sub>ss </sub></em><strong>on MATLAB Grader</strong>

<h3>Question 1.C – Simulation (MATLAB Online / Gradescope)</h3>

Let’s see if the gains for combined drifting and path tracking work. Implement our new controller using the provided simulator framework.

We have provided the 18m radius reference path, as well as the lower level functions that you have implemented several times by now. You only need to edit the file called <em>mainproblem </em><em>1c</em>.

<em>Provide two plots, one of the velocity states (U<sub>x</sub></em><em>, U<sub>y</sub></em><em>, r</em><em>) and one of our path tracking errors (Fig’s 2 &amp;4 in provided plotting script). Do the results match what you expected, based on our closed loop pole locations? Why or why not.</em>

<h1>Problem 2 – Reflection</h1>

You’ve completed your project. You’ve watched your lookahead and group controller executed on a real vehicle. You’re officially a vehicle dynamicist!

In the project, you developed feedforward and feedback controllers for steering Niki along a defined path. Having had a chance to try those controllers on the actual car, you now have additional information about the appropriateness of your design choices beyond what you could gain from simulation. We want you to reflect on your project experience in light of this new information. This should be an individual response, not a team response. If you do find something wrong in your code when answering the first question, however, you can (and should) point this out to your teammates.

With the data and video from your vehicle testing, let’s take a closer look at how your simulated performance compares to the actual performance on the vehicle.

<h2>Question 2.A – Reflection of Lookahead Controller (Gradescope)</h2>

We’ll start with a reflection on your lookahead controller. Let’s take a look at your code and make sure that everything was actually implemented correctly. A couple of teams had some implementation issues so, if your results seemed strange, check again that your code was written correctly.

Next, consider whether you think the amount of feedback and feedforward was appropriate. Feedforward enables you to lower feedback gains by adjusting the steering to the value you expect you need for a turn. It can, however, lead to errors if the feedforward steering is not exact (which is very possible if there is even a slight misalignment of the steering). Feedback – particularly proportional feedback – reduces the steady-state error but also makes the system response faster, potentially amplifying noise or the effects of delay.

<ul>

 <li><strong>Was everything implemented correctly? If not, what implementation challenges did your team run into?</strong></li>

 <li><strong>Did each of your controllers effectively use feedback and feedforward? Support your conclusion with plots of your performance.</strong></li>

</ul>

<h2>Question 2.B – Reflection of Group Controller (Gradescope)</h2>

Now let’s move on to your group’s controller. Let’s take a look at your code once more to make sure that everything was actually implemented correctly. Let’s again consider whether you think the amount of feedback and feedforward was appropriate in this case.

<ul>

 <li><strong>Was everything implemented correctly? If not, what implementation challenges did your team run into?</strong></li>

 <li><strong>Did each of your controllers effectively use feedback and feedforward? Support your conclusion with plots of your performance.</strong></li>

</ul>

<h2>Question 2.C – Reflection of Project (Gradescope)</h2>

Now that we’ve reflected on both the lookahead controller and your group’s controller, let’s reflect on what we’ve learned from the design, analysis, and testing of these controllers.

<ul>

 <li><strong>What did you take away from the project?</strong></li>

 <li><strong>What, if anything, is still unclear to you about the controllers you used or linear vehicle dynamics after this project?</strong></li>

</ul>