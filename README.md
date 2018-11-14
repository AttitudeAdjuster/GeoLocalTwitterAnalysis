# GeoLocalTwitterAnalysis
Geo-localised analysis of twitter feeds

We capture Twitter feeds based on a specific keyword list (could be hashtags)<br>
<b>Each tweet is analysed for sentiment and emotion in realtime <br></b>
The tweet+analysis+goe-coordinates are saved on a Cloudant database for further processing/display etc<br>
Only tweets with avalaible GeoCoordinates are considered<br>

### Example stream


#13 date/time: 2018-10-19/15:02:56 country: GB coords: [-5.928412999999999, 54.595869]
sentiment: {'score': -0.682805, 'label': 'negative'} emotion: {'sadness': 0.351108, 'joy': 0.200484, 'anger': 0.114318, 'disgust': 0.135275, 'fear': 0.189809}
text: Bye bye work and Brexit for 3 weeks, 🇬🇧🇪🇺🇺🇸<br>
#14 date/time: 2018-10-19/15:02:59 country: GB coords: [-1.7396195000000003, 55.13141850000001]
sentiment: {'score': -0.547404, 'label': 'negative'} emotion: {'sadness': 0.219415, 'joy': 0.075017, 'anger': 0.222991, 'disgust': 0.201936, 'fear': 0.309282}
text: Theresa May isolated as party turns on 'chaotic' Brexit plan and EU leaders give her the cold shoulder… https://t.co/TehqhqO4M3<br>
#15 date/time: 2018-10-19/15:03:28 country: IE coords: [-6.174398500000001, 53.257283]
sentiment: {'score': 0.0, 'label': 'neutral'} emotion: {'sadness': 0.410715, 'joy': 0.077877, 'anger': 0.066157, 'disgust': 0.101531, 'fear': 0.051428}
text: @DanielJHannan 7th now since the #Brexit Referendum<br>
#16 date/time: 2018-10-19/15:03:51 country: GB coords: [-1.5301095, 52.5428055]
sentiment: {'score': -0.446986, 'label': 'negative'} emotion: {'sadness': 0.178744, 'joy': 0.277558, 'anger': 0.021017, 'disgust': 0.097495, 'fear': 0.105677}
text: Let me know when it gets to 17.5m 👍🙄<br>
#17 date/time: 2018-10-19/15:04:03 country: DE coords: [13.4246065, 52.506701]
sentiment: {'score': -0.737863, 'label': 'negative'} emotion: {'sadness': 0.236995, 'joy': 0.032755, 'anger': 0.156737, 'disgust': 0.018282, 'fear': 0.721258}
text: @dave_odo @MeachamDave @Bandage22 @darrengrimes_ Nope. German car makers wake up worrying about AI, driverless vehi… https://t.co/ShLCe2l9Ir<br>
#18 date/time: 2018-10-19/15:04:20 country: GB coords: [-3.0044560000000002, 53.4698505]
sentiment: {} emotion: {}
text: Excellent. 👏👏👏👏<br>
#19 date/time: 2018-10-19/15:04:33 country: GB coords: [0.07886299999999999, 51.584990000000005]
sentiment: {'score': -0.677009, 'label': 'negative'} emotion: {'sadness': 0.563202, 'joy': 0.019351, 'anger': 0.384322, 'disgust': 0.217552, 'fear': 0.06397}
text: @Jacob_Rees_Mogg I know, Mr Mogg, this will delay you and the gutless fools you support, making a run for her job,… https://t.co/NrAcCro6gf<br>
#20 date/time: 2018-10-19/15:04:34 country: GB coords: [-1.2334335, 51.75428599999999]
sentiment: {'score': 0.0, 'label': 'neutral'} emotion: {'sadness': 0.407917, 'joy': 0.151966, 'anger': 0.190336, 'disgust': 0.162163, 'fear': 0.086128}
text: @Jacob_Rees_Mogg Any idea how much Brexit is and will cost the UK and people who run businesses? You seem to always… https://t.co/meX30hlRYx<br>


### Geo-localised and sentiment-tagged tweets are read from a Cloudant database and displayed as a heatmap <br>
![Brexit Heatmap](https://raw.githubusercontent.com/AttitudeAdjuster/GeoLocalTwitterAnalysis/master/img/Brexit_heatmap.png)



### A Machine Learnig model is fitted to the data and evaluated to test data
Aim: predict the sentiment given latitude/longitude<br>
If the model performance is acceptable on test data, we can use it for anomaly detection<br>
Incoming data can be compared to predictions and a lag is raised if an anomaly is detected<br>

<font face="Courier">
Training GBT model...<br>
Evaluating model on test data...<br>
+--------------------+---------+--------------------+<br>
|          prediction|    score|            features|<br>
+--------------------+---------+--------------------+<br>
|-0.02673812155075842|-0.888036|[-0.2161080000000...|<br>
|-0.16844047496706444| -0.81063|[110.333028,1.429...|<br>
|-0.16595070797070496| -0.75617|[-0.1091815,51.54...|<br>
|-0.08496630422360758| -0.72438|[-0.442361,51.537...|<br>
|-0.15084220913585722| -0.48417|[-0.0991635,51.64...|<br>
+--------------------+---------+--------------------+<br>
only showing top 5 rows<br>

Root Mean Squared Error (RMSE) on test data = 0.487036<br>
R2 on test data = -0.00110838<br>
</font>
This model is no better than random choice<br>

