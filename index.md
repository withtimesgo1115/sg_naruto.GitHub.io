Note: this page is just used to show our analysis work for Naruto World based on the skills we learned from the Social Network class.

# Story Origin
<div class="origin" style="text-align:justify; text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
Ninja is a well-known ancient profession in Japan. Their work includes protecting important people, sneaking into enemy camps to collect intelligence, performing secret missions, assassination activities, etc. This ancient profession in Japan is very similar to the military officer Jin Yiwei of the official intelligence agency of the Ming Dynasty in China, except that they have been given a more legendary color after the dramatic interpretation of artistic works. One of the most popular comics related to this topic is called <i>Naruto</i>, which tells a passionate, warm and inspirational ninja story. Therefore, our interest is to analyze the ninja world described in this comic by means of complex networks and natural language processing. Not much to say, let us walk into the world of Naruto together.
</div>

# Introduction
<div class="wrapper" style="hight:525px">
    <img src="./img/intro.jpg" style="float:left; margin: 10px;">
    <div style="position:relative; left:10px; text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
    This classic comic is developed around the fetters of the two protagonists <b>Naruto Uzumaki</b> and <b>Sasuke Uchiha</b>. The specific storyline will not be introduced in detail here, and interested friends can search by themselves. <i>Naruto</i> is a comic with a grand world, including a large number of characters and related concepts, which is very suitable for network analysis. Therefore, by constructing a complex network and performing basic network analysis, we can understand the number of characters, the out-degree, the in-degree, the nature of the network, and the network diagram based on the overall character connections. In this work, most ninja characters have corresponding ninja villages, clans and ninja levels. These different attributes divide the ninjas into different groups, and also imply a certain relationship between ninjas. Our research interest also includes whether the communities divided according to these attributes are consistent with the communities solved by the algorithm based on node connections. Apart from these goals, we also tried to find the wordcloud, calculate centrality and implement sentiment analysis, etc.   
    </div>
</div>
<div style="clear:both;"></div>

# Baisc Network Analysis
<div class="wrapper" style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
Our datasets are extracted from the Fandom wikipages by using the API provided by this website and some libraries such as JSON, urllib, and BeautifulSoup, etc. The first dataset is the text content of every character webpage shown in the comic. The second data set is the XXX. For the first dataset, we crawled the text length, affiliation and clan in each page as the attributes for the node. The network edges are generated according to the superlinks of corresponding node pages. After constructing the network, it is easy to obtain the number of nodes and edges by calling the built-in methods of NetworkX. The result shows there are <b>1293</b> nodes and <b>11055</b> edges and note that the isolated nodes that there is no connection between that node and others has been removed already.
</div>