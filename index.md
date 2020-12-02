Note: this page is just used to show our analysis work for Naruto World based on the skills we learned from the Social Network class.

# Story Origin
Ninja is a well-known ancient profession in Japan. Their work includes protecting important people, sneaking into enemy camps to collect intelligence, performing secret missions, assassination activities, etc. This ancient profession in Japan is very similar to the military officer Jin Yiwei of the official intelligence agency of the Ming Dynasty in China, except that they have been given a more legendary color after the dramatic interpretation of artistic works. One of the most popular comics related to this topic is called *Naruto*, which tells a passionate, warm and inspirational ninja story. Therefore, our interest is to analyze the ninja world described in this comic by means of complex networks and natural language processing. Not much to say, let us walk into the world of Naruto together.

# Introduction
<div class="wrapper" style="hight:525px">
    <img src="./img/intro.jpg" style="float:left; margin: 10px;">
    <div style="position:relative; left:10px; text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
    This classic comic is developed around the fetters of the two protagonists Naruto Uzumaki and Sasuke Uchiha. The specific storyline will not be introduced in detail here, and interested friends can search by themselves. <i>Naruto</i> is a comic with a grand world, including a large number of characters and related concepts, which is very suitable for network analysis. Therefore, by constructing a complex network and performing basic network analysis, we can understand the number of characters, the out-degree, the in-degree, the nature of the network, and the network diagram based on the overall character connections. In this work, most ninja characters have corresponding ninja villages, clans and ninja levels. These different attributes divide the ninjas into different groups, and also imply a certain relationship between ninjas. Our research interest also includes whether the communities divided according to these attributes are consistent with the communities solved by the algorithm based on node connections. Apart from these goals, we also tried to find the wordcloud, calculate centrality and implement sentiment analysis, etc.   
    </div>
</div>
<div style="clear:both;"></div>

# Baisc Network Analysis