# Description
A2.ibynd takes an input of letters and touchpoints and uses spatial and language models to generate a most probable string and direct string output. 

# Mathematical Models
A2 uses the following spatial and language models

<a href="https://www.codecogs.com/eqnedit.php?latex=P(w|s_1,s_2,...s_n)&space;=&space;\frac{P(s_1,s_2,...s_n|w)P(w)}{p(s_1,s_2,...s_n)}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(w|s_1,s_2,...s_n)&space;=&space;\frac{P(s_1,s_2,...s_n|w)P(w)}{p(s_1,s_2,...s_n)}" title="P(w|s_1,s_2,...s_n) = \frac{P(s_1,s_2,...s_n|w)P(w)}{p(s_1,s_2,...s_n)}" /></a>

## Spatial model
For every word which shares the same length as the given set of touchpoints, A2 uses a dual Guassian spatial model:

<a href="https://www.codecogs.com/eqnedit.php?latex=P(s_i|c_i)&space;=&space;P(s_i|\mu,\sigma^2)&space;=&space;\frac{1}{(2\pi\sigma^2)^{1/2}}exp(-\frac{1}{2\sigma^2}(s-\mu)^2)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(s_i|c_i)&space;=&space;P(s_i|\mu,\sigma^2)&space;=&space;\frac{1}{(2\pi\sigma^2)^{1/2}}exp(-\frac{1}{2\sigma^2}(s-\mu)^2)" title="P(s_i|c_i) = P(s_i|\mu,\sigma^2) = \frac{1}{(2\pi\sigma^2)^{1/2}}exp(-\frac{1}{2\sigma^2}(s-\mu)^2)" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=\sigma^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sigma^2" title="\sigma^2" /></a> represents a diagional covariance matrix where:

<a href="https://www.codecogs.com/eqnedit.php?latex=\sigma^2_x&space;=&space;a&space;&plus;&space;b&space;*&space;W^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sigma^2_x&space;=&space;a&space;&plus;&space;b&space;*&space;W^2" title="\sigma^2_x = a + b * W^2" /></a>
and 
<a href="https://www.codecogs.com/eqnedit.php?latex=\sigma^2_y&space;=&space;c&space;&plus;&space;d&space;*&space;H^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sigma^2_y&space;=&space;c&space;&plus;&space;d&space;*&space;H^2" title="\sigma^2_y = c + d * H^2" /></a>

## Language model
A2 uses a dictionary in *unigram.dict* which is multiplied with the spatial model as described above.
For each word, A2 parses through the dictionary and finds words that appear to be suitable based on the given touchpoints, thus reducing the processing time.

# How to use
In the first block of A2 on the third line, change the file location to match your data. **make sure your data file follows the same writing convention** of</br> 
"===Word x===</br>
y 33 22</br>
w 12.222 1.111</br>
===Word z===</br>
w 12.222 1.111"</br>

Run the program and expect to wait awhile for it to process. On my machine it takes about 40 seconds per word.

The output will be available in a newly generated results.txt which displays the accuracy of the decoded words, and the accuracy of the raw string. This first line is then followed by each words: correct_word, decoded_word, and literal_string