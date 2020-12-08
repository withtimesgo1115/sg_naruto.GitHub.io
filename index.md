Note: this page is just used to show our analysis work for Naruto World based on the skills we learned from the Social Network class.

# Story Origin
<div class="origin" style="text-align:justify; text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
Ninja is a well-known ancient profession in Japan. Their work includes protecting important people, sneaking into enemy camps to collect intelligence, performing secret missions, assassination activities, etc. This ancient profession in Japan is very similar to the military officer Jin Yiwei of the official intelligence agency of the Ming Dynasty in China, except that they have been given a more legendary color after the dramatic interpretation of artistic works. One of the most popular comics related to this topic is called <i>Naruto</i>, which tells a passionate, warm and inspirational ninja story. Therefore, our interest is to analyze the ninja world described in this comic by means of complex networks and natural language processing. Not much to say, let us walk into the world of Naruto together.
</div>

# Introduction
<div class="wrapper" style="hight:525px">
    <img src="./img/intro.jpg" style="float:left; margin: 10px;">
    <div style="position:relative; left:10px; text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
    This classic comic is developed around the fetters of the two protagonists <b>Naruto Uzumaki</b> and <b>Sasuke Uchiha</b>. The specific storyline will not be introduced in detail here, and interested friends can search by themselves. <i>Naruto</i> is a comic with a grand world, including a large number of characters and related concepts, which is very suitable for network analysis. Therefore, by constructing a complex network and performing basic network analysis, we can understand the number of characters, the out-degree, the in-degree, the nature of the network, and the network diagram based on the overall character connections. In this work, most ninja characters have corresponding ninja villages and graudation age from the ninja academy. The attribute ninja village divides the ninjas into different groups, and also imply a certain relationship between ninjas and the attribute graduation age shows the ninja's talent in a way. Our research interest includes whether the communities divided according to the village attribute are consistent with the communities solved by the algorithm based on node connections. Apart from these goals, we also tried to find the wordcloud, calculate centrality, implement sentiment analysis but the most fun is to research if geniuses are all alone, whether they change the world, sentiment analysis in terms of villages, find the sentiment variation of Sasuke (One of the two protagonists) over paragraphs and implement character pairing analysis.   
    </div>
</div>
<div style="clear:both;"></div>

# Network Analysis
<div class="wrapper" style="margin:10px;text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
Our datasets are extracted from the Fandom wikipages by using the API provided by this website and some libraries such as JSON, urllib, and BeautifulSoup, etc. The first dataset is the text content of every character webpage shown in the comic. The second data set is the light novels of this comic. For the first dataset, we crawled the villages and graduation age in each character page as the attributes for the node. The network edges are generated according to the superlinks of corresponding node pages. After constructing the network, it is easy to obtain the number of nodes and edges by calling the built-in methods of NetworkX. The result shows there are <b>1324</b> nodes and <b>11056</b> edges and note that the isolated nodes that there is no connection between that node and others has been removed already.
</div>

## Degree Analysis
<div>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
        The degree of a node in the network is the number of adjacent nodes that the i-th node has, which is the simplest but most important feature. The greater the degree, the more important the node is to some extent. For directed networks, degrees are divided into two categories: out-degree and in-degree. Out-degree refers to the number of edges from current node to other node. In-degree refers to the number of edges from other node to current node. 
        Once the network generated successfully, the degree analysis will not be complex since the third-party library <i>NextwrokX</i> provides us with a lot of methods. From the figure below, you can see the top 5 nodes in terms of the number of out-degree and in-degree. The result is basically consistent with our expected result. They are indeed the most important characters in this comic. However, the appearance of "Naruto Musasabi" is out of our expectation that this character occupies the third place in the in-degree rank list. We found that this character is a fictional character from a novel written by a real character Jiraiya and this character is protagonist Naruto Uzumaki's namesake, which makes it own high in-degree. At the same time, the in-degree value greater than the out-degree value can also be explained, because most small characters will cite several important characters, but they are rarely cited by other characters, which leads to a very large in-degree of important characters. 
    </p>
    <img src="./img/new_top5.png" style="margin:10px;"/>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
        Here for both distribution, the bins are 100. We used 'Frequency' as y-label here, according to the given example in lecture 4.
    </p>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
        For in-degree distribution, most of the values are distributed between 0 and 50(more exactly, 0 to 20). There are limited nodes with extremely high in-degrees in the network, which means that the tail of this power-law distribution(long-tail distribution) will be pretty long. From the figure of out-degree distribution, the conclusion can be obtained that unlike the case of in-degrees, many nodes own non-zero out-degree values. Besides, the variance of out-degree frequency is considerable smaller than that of in-degree one and there aren't many outliers.
    </p>
    <img src="./img/new_degrees.png" />
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
    Clearly, for Naruto degree distribution, it looks like power-law distribution. Most nodes have links between 0 and 50 and a few of them have a considerable number of links. The nodes with high degree value are those who have high in-degrees. These protagonists can be considered as hubs in the network.
    For ER random network, it obeys binominal distribution and can be thought as Poisson Distribution roughly because we have a large number of nodes. Most degrees are distributed between 10 and 25.
    </p>
    <img src="./img/new_compare.png" />
</div>

## Centrality Analysis
<div>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
    Centrality analysis can help us to find the most important node in the network and in our analysis, three different methods for calculating the centrality are used; they are <b>degree centrality</b>，<b>betweenness centrality</b> and <b>eigenvector centrality</b> respectively. The results are shown in the figure below.
    </p>
    <img src="./img/new_centrality.png">
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
    The leftest figure is obtained by using the degree centrality, the middle one shows the centrality based on the betweenness centrality and the result of egienvector centrality can be found in the rightest figure. From these figures, it is obvious that the top 3 characters in terms of centrality are Naruto Uzumaki, Kakashi Hatake and Sasuke Uchiha according to all 3 methods, which fits our expectations perfectly. However, the fourth and fifth characters found are a bit different. the heroine Sakura Haruno and Naruto's sakename Naruto Musasabi appear twice each and meanwhile one of the most important villains named Orochimaru and absolute protagonist's son Boruto Uzumaki show up once. This difference comes from the solving logic of different algorithm and more details are given in our explainer notebook. Overall, the results are reasonable because they are all key characters whose story runs through the whole work.       
    </p>
</div>

## Community Analysis
<div>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
    Here, you can find all 9 communities givne by <i>Louvain Method</i> in the community distribution figure. The x-axis represents the sequence number of each community and the y-axis represents the number of nodes for that community.  
    </p>
    <img src="./img/communities.png" style="float:left; margin-right: 30px;">
    <table style="width:50%; height: 300px;">
        <tr>
            <th></th>
            <th><b>Community</b></th>
        </tr>
        <tr>
            <td>0</td>
            <td>Kabuto Yakushi & Might Guy & Kurama</td>
        </tr>
        <tr>
            <td>1</td>
            <td>Tsunade & Jiraiya & Nagato</td>
        </tr>
        <tr>
            <td>2</td>
            <td>Naruto Uzumaki & Kakashi Hatake & Sasuke Uchiha</td>
        </tr>
        <tr>
            <td>3</td>
            <td>Sakura Haruno & Gaara & Shikamaru Nara</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Sai & Kankurō & Sasori</td>
        </tr>
        <tr>
            <td>5</td>
            <td>Boruto Uzumaki & Mitsuki & Sarada Uchiha</td>
        </tr>
        <tr>
            <td>6</td>
            <td>Orochimaru & Kimimaro & Guren</td>
        </tr>
        <tr>
            <td>7</td>
            <td>Itachi Uchiha & Danzō Shimura & Minato Namikaze</td>
        </tr>
        <tr>
            <td>8</td>
            <td>Shabadaba & Haido & Hikaru Tsuki</td>
        </tr>
    </table>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;overflow:hidden;">
    Besides, we named every community using three character names whose degree ranks in top 3 in that community. In the row 2, you can see Naruto, Kakashi and Sasuki are grouped to the same community and other communities also meet our expectation. You can find the result in the table above.
    </p>
</div>

## Network Overview
<p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word;">
    The overall network of Naruto World is shown in the figures below. As shown in the figure, those nodes whose size is obviously larger than others are critical protagonists in the network. They have higher degrees. The connections(links) among these nodes are drawn in shallow yellow. 
</p>
<div style="display:flex">
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    The first network graph is drawn based on the <b>communities</b> analyzed above. Different node is grouped in a different community with different colors.
    </p>
    <img src="./img/network.jpg" style="display:flex; justify-content:center; align-items:center;"/>
</div>

<div style="display:flex">
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    The first network graph is drawn based on the <b>clan</b> extracted from the wikipages in the beginning. Different node is grouped in a different clan with different colors. There are 42 clans in this comic so that you can see 42 different colors marking the nodes.
    </p>
    <img src="./img/clan.png" style="display:flex; justify-content:center; align-items:center; "/>
</div>

# Text Analysis
<p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    In this section, the research based on the text analysis is introduced which contains sentiment analysis, wordcloud processing, novel analysis etc.   
</p>

## Wordcloud Generation
<div>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    The wordcloud generated through <i>TF-IDF</i> is shown in the figure below. From that, you can see the more important for the word, the bigger the word is so that <b>Naruto</b>, <b>Sasuki</b>, and <b>Boruto</b>, etc. are much bigger than other words because they are all the main characters' names. Meanwhile, it is noticeable that <b>team</b>, <b>village</b>, <b>attack</b>, <b>mission</b> and so on are also high-frequent. This can be explained by the key value of this comic(or anime): team up to execute all kinds of mission to maintain the peace, attack the intruder and protect the village.   
    </p>
    <img src="./img/newwordcloud.png"/>
</div>

## Sentiment Analysis
<p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    The sentiment analysis aims to find the happiest and saddest character in this comic and we used a sentiment dataframe provided to calculate the sentiment values for each character. In the sentiment reference dataframe, all the words have happiness rank and corresponding happiness mean value which can be used to obtain the overall mean sentiment value for each character's wikipage. After the calculation, we can find the sentiment values for every character and then rank them in descending order(the bigger sentiment value means happier the character is).     
</p>
<div>
    <img src="./img/new_sentiment.png"/>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    It is obvious that the sentiment values do not change much and fluctuate within a limited range. Most of the sentiment values of the characters are between 5.4 and 5.5 and it looks like a normal distribution. The result is shown in the figure above.
    </p>
</div>
<div>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    After sorting the sentiment values, it is not hard to find the top 5 happiest characters as well as the saddest characters. Let's have a look in the tables below.
    </p>
    <table style="float:left; width: 50%; height:400px;">
        <tr>
            <th><b>top 5 happiest</b></th>
            <th><b>chatracter</b></th>
            <th><b>sentiment</b></th>
        </tr>
        <tr>
            <td>0</td>
            <td>Himawari Uzumaki</td>
            <td>5.786766</td>
        </tr>
        <tr>
            <td>1</td>
            <td>Asura Ōtsutsuki</td>
            <td>5.753659</td>
        </tr>
        <tr>
            <td>2</td>
            <td>Kushina Uzumaki</td>
            <td>5.740877</td>
        </tr>
        <tr>
            <td>3</td>
            <td>Hamura Ōtsutsuki</td>
            <td>5.733134</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Hagoromo Ōtsutsuki</td>
            <td>5.722735</td>
        </tr>
    </table>
    <table style="width: 50%; hight: 400px;">
        <tr>
            <th><b>top 5 saddest</b></th>
            <th><b>chatracter</b></th>
            <th><b>sentiment</b></th>
        </tr>
        <tr>
            <td>0</td>
            <td>Hidan</td>
            <td>5.172518</td>
        </tr>
        <tr>
            <td>1</td>
            <td>Gyūki</td>
            <td>5.215784</td>
        </tr>
        <tr>
            <td>2</td>
            <td>Rōshi</td>
            <td>5.241013</td>
        </tr>
        <tr>
            <td>3</td>
            <td>Zabuza Momochi</td>
            <td>5.254157</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Kina Kodon</td>
            <td>5.258733</td>
        </tr>
    </table>
    <div style="clear:both;"></div>
    <p style="margin-top: 30px;">
    According to the table we found, the happiest character is <b>Himawari Uzumaki</b> while the saddest character is <b>Hidan</b>. This difference comes from the truth that the wikipage of Himawari Uzumaki contains a number of words with a high sentiment but Hidan's wikipage is opposite. However, is our guess correct? How to verify? This is a small challenge for us so a short script is written which can be used to evaluate the corresponding word counts in terms of its sentiment values for each wikipage text. Finally, we found there are <b>father</b>, <b>brother</b> and <b>mother</b> and so on showing up above 20 times in the wikipage of the happiest character. On the other hand, the saddest character "Hidan"'s page contains terrible words like <b>kill</b> even reaching an astonishing 17 times. This can be explained by the story about these two characters. The happiest character is only a 10-year old little girl who borned after the world returning to peace (in the end of the story), we have abundant reason to believe that she is the happiest character in Naruto. However, for the saddest one, he is a villain who has killed many ninjas through the story because he adores death. 'Kill' is a very sad word in our analysis, but for Hidan, it's the source of his happiness. You can find the evidence in the tables below.
    </p>
    <table style="float:left; width:50%;">
        <tr>
            <th><b></b></th>
            <th><b>word</b></th>
            <th><b>counts</b></th>
            <th><b>sentiment</b></th>
        </tr>
        <tr>
            <td>0</td>
            <td>father</td>
            <td>26</td>
            <td>7.06</td>
        </tr>
        <tr>
            <td>1</td>
            <td>brother</td>
            <td>21</td>
            <td>7.22</td>
        </tr>
        <tr>
            <td>2</td>
            <td>mother</td>
            <td>20</td>
            <td>7.68</td>
        </tr>
        <tr>
            <td>3</td>
            <td>home</td>
            <td>14</td>
            <td>7.14</td>
        </tr>
        <tr>
            <td>4</td>
            <td>13</td>
            <td>18</td>
            <td>6.24</td>
        </tr>
    </table>
    <table style="width:50%;">
        <tr>
            <th><b></b></th>
            <th><b>word</b></th>
            <th><b>counts</b></th>
            <th><b>sentiment</b></th>
        </tr>
        <tr>
            <td>0</td>
            <td>opponent</td>
            <td>20</td>
            <td>3.90</td>
        </tr>
        <tr>
            <td>1</td>
            <td>kill</td>
            <td>17</td>
            <td>1.56</td>
        </tr>
        <tr>
            <td>2</td>
            <td>body</td>
            <td>16</td>
            <td>5.96</td>
        </tr>
        <tr>
            <td>3</td>
            <td>despite</td>
            <td>13</td>
            <td>4.48</td>
        </tr>
        <tr>
            <td>4</td>
            <td>battle</td>
            <td>13</td>
            <td>2.98</td>
        </tr>
    </table>
</div>

## Original Analysis
<p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
In this section, we will show the most interesting research topics. The research in this section combines all the theoretical knowledge and analyzing skills we learned in the course to mine hidden information contained in the network and texts and to compare the results we obtained with the conventional cognition. Complex network and natural language processing are both for discovering, explaining and then solving practical problems in life, instead of just doing some analysis alone. 
</p>

### Question 1: Are geniuses all alone? / Are geniuses changing the world?
<p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
In Naruto world, every child in Ninja Villages will be admitted to the Ninja Academy to learn basic ninjutsu (the skills to become a ninja) at a very young age. Only graduating successfully from these academies, they were considered professional ninjas. In most cases, gifted children will graduate at an early age and this is also match the situation in our real world. In line with our experience, the centrality of a character reflects the importance in the comic world. Out-degree illustrates how much one cares about other characters. In-degree demonstrates one's degree of being noticed. Therefore, to solve this question, we made an investigation regarding the characters with young graduation age(they are geniuses) and their degree and eigenvector centrality and this should rely on the graduation age attribute collected in the previous steps. 
</p>
<div>
    <img src="./img/graduation_age.png"/>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    From the figure of graduation age distribution, it is not hard to find that most ninjas graduate at 12 years old and the Naruto Uzumaki also belong to this group because he is not a talented ninja although he is very hard-working and ambitious. Only a few real geniuses become professional ninjas before their 9th birthday. These characters should be considered here.
    </p>
</div>
<div>
    <table>
        <tr>
            <th><b></b></th>
            <th><b>Name</b></th>
            <th><b>Graduation age</b></th>
            <th><b>In-degree</b></th>
            <th><b>Out-degree</b></th>
            <th><b>Eigenvector centrality</b></th>
        </tr>
        <tr>
            <td>0</td>
            <td>Kakashi Hatake</td>
            <td>5</td>
            <td>247</td>
            <td>108</td>
            <td>0.220451</td>
        </tr>
        <tr>
            <td>1</td>
            <td>Jiraiya</td>
            <td>6</td>
            <td>128</td>
            <td>58</td>
            <td>0.132034</td>
        </tr>
        <tr>
            <td>2</td>
            <td>Orochimaru</td>
            <td>6</td>
            <td>194</td>
            <td>65</td>
            <td>0.197742</td>
        </tr>
        <tr>
            <td>3</td>
            <td>Naruto Musasabi</td>
            <td>6</td>
            <td>2476</td>
            <td>8</td>
            <td>0.178412</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Tsunade</td>
            <td>6</td>
            <td>143</td>
            <td>60</td>
            <td>0.136061</td>
        </tr>
        <tr>
            <td>5</td>
            <td>Yamato</td>
            <td>6</td>
            <td>65</td>
            <td>55</td>
            <td>0.098044</td>
        </tr>
        <tr>
            <td>6</td>
            <td>Itachi Uchiha</td>
            <td>7</td>
            <td>117</td>
            <td>41</td>
            <td>0.129140</td>
        </tr>
        <tr>
            <td>7</td>
            <td>Might Guy</td>
            <td>7</td>
            <td>103</td>
            <td>64</td>
            <td>0.117126</td>
        </tr>
        <tr>
            <td>8</td>
            <td>Sasori</td>
            <td>7</td>
            <td>57</td>
            <td>31</td>
            <td>0.072870</td>
        </tr>
        <tr>
            <td>9</td>
            <td>Baki</td>
            <td>8</td>
            <td>13</td>
            <td>20</td>
            <td>0.026534</td>
        </tr>
    </table>
    <p>
    From the table above, we can see most geniuses are important characters in the comic. Kakashi(Naruto's supervisor), Jiraiya(Naruto's master) and Itachi Uchiha(Sasuke Uchiha's brother) etc. help to promote the development of the storyline and their centrality values, degree values are all high compared with normal characters which means they change the world to some extent. As for social relationship of these geniuses, Kakashi Hatake has a number of friends while Naruto Musasabi seems to not care about others since his out-degree is only 8. Besides, Baki is a real genius, but with little attention. Overall, in the usual case, being a genius doesn't bring loneliness. Genius is not always alone.
    </p>
</div>

### Question 2: Ninjas from which village are the saddest?
<p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
The dog-eat-dog world in Naruto is cruel and filled with tragedy. Without power above all, there are wars between countries(more accurately it's between villages because each country built a ninja village to train ninjas as military forces) every year. The five largest villages, Konohagakure, Kirigakure, Kumogakure, Iwagakure, and Sunagakure tend to choose small villages as battlefields, resulting in the expansion of hatred and sadness. One of the most powerful villains in Naruto comes from a small village, he destroyed the hometown of Naruto Uzumaki, for revenge. In short, the world is stuck in a circle of avenge and revenge. Both the villains and heroes aim at bringing peace back to the world. Villains plan to become the power above all to eliminate all the unstable factors. Heroes know that the length of peace kept by force would be the length of the ruler's life. It's not a long-term plan. Thus they determine to unite the world by love.
In this question, we would like to find out the village with the most tragedy. Our guess would be Amegakure. As a small village between three great countries, it has frequently served as a battleground during the various ninja wars, making most of its population war refugees. The following analysis will evaluate our guess.
</p>
<div>
    <img src="./img/villages_sentiment.png"></img>
</div>
<div>
    <table>
        <tr>
            <th><b></b></th>
            <th><b>Village</b></th>
            <th><b>Sentiment</b></th>
        </tr>
        <tr>
            <td>0</td>
            <td>Yugakure</td>
            <td>5.191124</td>
        </tr>
        <tr>
            <td>1</td>
            <td>Ishigakure</td>
            <td>5.278589</td>
        </tr>
        <tr>
            <td>2</td>
            <td>Shangri-la</td>
            <td>5.306823</td>
        </tr>
        <tr>
            <td>3</td>
            <td>Howling Wolf Village</td>
            <td>5.324129</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Kumogakure</td>
            <td>5.367670</td>
        </tr>
        <tr>
            <td>6</td>
            <td>Kirigakakure</td>
            <td>5.371250</td>
        </tr>
        <tr>
            <td>13</td>
            <td>Iwagakure</td>
            <td>5.421362</td>
        </tr>
        <tr>
            <td>18</td>
            <td>Sunagakure</td>
            <td>5.449992</td>
        </tr>
        <tr>
            <td>21</td>
            <td>Konohagakure</td>
            <td>5.488923</td>
        </tr>
    </table>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    Note that living in the 5 great villages, Konohagakure, Kirigakure, Kumogakure, Sunagakure, and Iwagakure usually doesn't mean a relatively safe. Great countries could also be destroyed easily by wars.
    </p>
</div>
<div>
    <table style="float:left; width:50%;">
        <tr>
            <th><b></b></th>
            <th><b>word</b></th>
            <th><b>counts</b></th>
            <th><b>sentiment</b></th>
        </tr>
        <tr>
            <td>0</td>
            <td>beast</td>
            <td>218</td>
            <td>3.36</td>
        </tr>
        <tr>
            <td>1</td>
            <td>ha</td>
            <td>155</td>
            <td>6.00</td>
        </tr>
        <tr>
            <td>2</td>
            <td>attack</td>
            <td>145</td>
            <td>2.42</td>
        </tr>
        <tr>
            <td>3</td>
            <td>one</td>
            <td>121</td>
            <td>5.40</td>
        </tr>
        <tr>
            <td>4</td>
            <td>war</td>
            <td>107</td>
            <td>1.80</td>
        </tr>
    </table>
    <table style="width: 50%;">
        <tr>
            <th><b></b></th>
            <th><b>word</b></th>
            <th><b>counts</b></th>
            <th><b>sentiment</b></th>
        </tr>
        <tr>
            <td>0</td>
            <td>team</td>
            <td>1926</td>
            <td>6.26</td>
        </tr>
        <tr>
            <td>1</td>
            <td>ha</td>
            <td>1735</td>
            <td>6.00</td>
        </tr>
        <tr>
            <td>2</td>
            <td>time</td>
            <td>1272</td>
            <td>5.74</td>
        </tr>
        <tr>
            <td>3</td>
            <td>one</td>
            <td>1268</td>
            <td>5.40</td>
        </tr>
        <tr>
            <td>4</td>
            <td>village</td>
            <td>1257</td>
            <td>6.28</td>
        </tr>
    </table>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    We noticed that beast appeared frequently in Kumogakure's text. Tailed beasts are 9 powerful monsters in Naruto. They were sealed in 9 human bodies(jinchūriki) in the five great countries. When a jinchūriki loses control of his/her tailed beast, the consequence would be disastrous: an out-of-control tailed beast would destroy everything until some powerful ninja stops it and seals it again. Therefore, the tailed beast may be the vital reason for the sadness in Kumogakure. Konohagakure is the most powerful village in the world and it's the hometown of the main characters. That's why Konohagakure is the happiest village among the great-5.
    </p>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    We found that ninjas from Yugakure are saddest. Actually, the saddest character, Hidan, is from Yugakure. Ironically, Yugakure is a small village which has strong inclinations towards pacifism. Ideally, it ought to be the happiest village in the world. However, Yugakure's transformation from a military force was not supported by all, Hidan being a notable objector. He slaughtered many villagers and left the village. Hidan has a very negative influence on the sentiment of Yugakure.
    </p>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    <b>WAR IS CRUEL</b>. In the world of Naruto, no matter great or small villages, they all face the pressure of war every day. It's so ironic that villagers in Yugakure, who love peace the most, are through the worst. We are supposed to cherish the peaceful time which got through difficult struggles: war has never been far away from us.
    </p>
</div>

### Question 3: Ninjas from which village are the saddest?
<div>
    <p style="text-align:justify;text-justify:inter-ideograph; word-wrap:break-word; align-items:center;">
    Let's have a glance at the light novel Sasuke Shinden: The Teacher's Star Pupil. It's fanfiction thus the information it gives may more or less reflect the ideas from fans. To start, we would simply compute the hero Saseke's sentiment change over paragraphs.
    </p>
</div>

# Download our dataset to play around & See our explainer notebook for more details 
Click here to find our data set: <a href="https://github.com/withtimesgo1115/sg_naruto.GitHub.io">Data Set</a>
<br>
Click here to find our explainer notebook: <a href="https://colab.research.google.com/drive/1qCEBo81UXYC43Q30sA5t5BdqYRldFBes#scrollTo=Xw7YTKMoB9uE">Explainer Notebook</a>