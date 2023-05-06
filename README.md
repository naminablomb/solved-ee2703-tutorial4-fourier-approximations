Download Link: https://assignmentchef.com/product/solved-ee2703-tutorial4-fourier-approximations
<br>
We will fit two functions, exp(<em>x</em>) and cos(cos(<em>x</em>)) over the interval [0<em>,</em>2<em>π</em>) using the fourier series

<em>a</em>                                                          (1)

<em>n</em>=1

As you know from earlier courses, the coefficients <em>a<sub>n </sub></em>and <em>b<sub>n </sub></em>are given by

<em>a</em><em>dx</em>

<em>a<sub>n        </sub></em><em>dx</em>

<em>b<sub>n        </sub></em><em>dx</em>

<ol>

 <li>Define Python functions for the two functions above, that take a vector (or scalar) input, and return avector (or scalar) value. Plot the functions over the interval [−2<em>π</em><em>,</em>4<em>π</em>) in Figure 1 and 2 respectively. Determine whether the functions are periodic. What function do you expect to be generated by the fourier series? Compute and plot those functions as well in the respective figures.</li>

</ol>

Note: Since exp(<em>x</em>) grows rapidly, use semilogy for that plot.

Note: Add grids and labels to figures.

<ol start="2">

 <li>Obtain the first 51 coefficients for the two functions above. Note: The built in integrator in Python integrates a scalar function from <em>a </em>to <em>b</em>. So you will have to compute the coefficients in a for loop. Also note that you will have to create two new functions to be integrated, namely <em>u</em>(<em>x</em><em>,k</em>) = <em>f</em>(<em>x</em>)cos(<em>kx</em>) and <em>v</em>(<em>x</em><em>,k</em>) = <em>f</em>(<em>x</em>)sin(<em>kx</em>). To integrate these, use the option in <em>quad </em>to pass extra arguments to the function being integrated:</li>

</ol>

rtnval=quad(u,0,2*pi,args=(k))

What this does is it accepts a function <em>u</em>(<em>x</em><em>,…</em>); the integration is over <em>x</em>, but the <em>k </em>values is passed to the function by quad as the second argument. So you will have to define the two functions as having <em>k </em>as their second (not first) argument.

<ol start="3">

 <li>For each of the two functions, make two different plots using “semilogy” and “loglog” and plot themagnitude of the coefficients vs <em>n</em>. The values should be plotted with red circles. Note that the answer should be a vector of the form</li>

</ol>

 <em>a</em><sub>0 </sub>

 <em>a</em><sub>1 </sub>

 

 <em>b</em><sub>1 </sub>

 <em>… </em>



 

 <em>a</em>25  <em>b</em>25

Note: Plot the coefficients for <em>f</em><sub>1</sub>(<em>x</em>) = exp(<em>x</em>) in Figures 3 and 4, and the coefficients for <em>f</em><sub>2</sub>(<em>x</em>) = cos(cos<em>x</em>) in Figures 5 and 6.

<ul>

 <li>If you did Q1 correctly, the <em>b<sub>n </sub></em>coefficients in the second case should be nearly zero. Why does this happen?</li>

 <li>In the first case, the coefficients do not decay as quickly as the coefficients for the second case.Why not?</li>

 <li>Why does <em>loglog </em>plot in Figure 4 look linear, wheras the <em>semilog </em>plot in Figure 5 looks linear?</li>

</ul>

<ol start="4">

 <li>We instead do a “Least Squares approach” to the problem. Define a vector <em>x </em>going from 0 to 2<em>π </em>in 400 steps (remember <em>linspace</em>). Evaluate the function <em>f</em>(<em>x</em>) at those <em>x </em>values and call it <em>b</em>. Now this function is to be approximated by Eq. (1). So for each <em>x<sub>i </sub></em>we want</li>

</ol>

<table width="531">

 <tbody>

  <tr>

   <td colspan="3" width="441">                                                              25                                    25<em>a</em><sub>0</sub>+ ∑ <em>a<sub>n </sub></em>cos<em>nx<sub>i </sub></em>+ ∑ <em>b<sub>n </sub></em>sin<em>nx<sub>i </sub></em>≈ <em>f</em>(<em>x<sub>i</sub></em>)</td>

   <td rowspan="2" width="44"> </td>

   <td rowspan="2" width="30"> </td>

   <td rowspan="2" width="15">(2)</td>

  </tr>

  <tr>

   <td width="183">Turn this into a matrix problem:</td>

   <td width="29"><em>n</em>=1</td>

   <td width="229"><em>n</em>=1</td>

  </tr>

  <tr>

   <td rowspan="2" width="183">             <sup> </sup>1     cos<em>x</em><sub>1                  </sub>sin<em>x</em><sub>1</sub> 1 cos<em>x</em><sub>2 </sub>sin<em>x</em><sub>2 </sub><sup> </sup><em>… … …</em>1       cos<em>x</em>400 sin<em>x</em>400</td>

   <td rowspan="2" width="29"><em>…</em><em>…</em><em>… …</em></td>

   <td rowspan="2" width="229"><em>a</em><sub>0</sub>1cos25<em>x</em><sup>2                       </sup>sin25<em>x</em>2  <em>…</em><em>b</em>1 <sub> </sub>= <sub></sub><em>…                          … </em> cos25<em>x</em>400 sin25<em>x</em>400  <em>a</em>25 <em>b</em>25</td>

   <td width="44"><em>f</em>(<em>x</em><sub>1</sub>) <em>f</em>(<em>x</em><sub>2</sub>) <em>…</em></td>

   <td width="30"></td>

   <td rowspan="2" width="15"> </td>

  </tr>

  <tr>

   <td colspan="2" width="74"><em>f</em>(<em>x</em><sub>400</sub>)</td>

  </tr>

 </tbody>

</table>

Create the matrix on the left side and call it <em>A</em>. We want to solve

<em>Ac </em>= <em>b</em>

where <em>c </em>are the fourier coefficients.

Note: The matrix can be constructed using zeros((400,51)) and then filling in the columns in a for loop. Do not use a double for loop. Here is the way to build up <em>x</em>, <em>b </em>and <em>A </em>without using nested loop:

x=linspace(0,2*pi,401) x=x[:-1] # drop last term to have a proper periodic integral b=f(x)             # f has been written to take a vector A=zeros((400,51))             # allocate space for A

A[:,0]=1             # col 1 is all ones for k in range(1,26):

A[:,2*k-1]=cos(k*x) # cos(kx) column

A[:,2*k]=sin(k*x)                      # sin(kx) column

#endfor

c1=lstsq(A,b)[0]               # the ’[0]’ is to pull out the # best fit vector. lstsq returns a list.

<ol start="5">

 <li>Use <em>lstsq </em>to solve this problem. You execute c=lstsq(A,b)[0]</li>

</ol>

What this does is to find the “best fit” numbers that will satisfy Eq. (2) at exactly the points we have evaluated <em>f</em>(<em>x</em>). Obtain the coefficients for both the given functions. Plot them with green circles in the corresponding plots.

<ol start="6">

 <li>Compare the answers got by least squares and by the direct integration. Do they agree? Should they?How much deviation is there (find the absolute difference between the two sets of coefficients and find the largest deviation. How will you do this using vectors?)</li>

 <li>Compute <em>Ac </em>from the estimated values of <em>c</em>. These should be the function values at <em>x<sub>i</sub></em>. Plot them (with green circles) in Figures 1 and 2 respectively for the two functions. Why is there so much deviation in Figure 1 but nearly perfect agreement in Figure 2?</li>

 <li>Write a report on this assignment in latex and submit the same along with your code.</li>

</ol>