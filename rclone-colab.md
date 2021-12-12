[Get started](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fwhy-you-should-try-rclone-with-google-drive-and-colab-753f3ec04ba1&source=post_page-----753f3ec04ba1---------------------nav_reg--------------)

[Open in app](https://rsci.app.link/?%24canonical_url=https%3A%2F%2Fmedium.com%2Fp%2F753f3ec04ba1&%7Efeature=LoOpenInAppButton&%7Echannel=ShowPostUnderCollection&%7Estage=mobileNavBar&source=post_page-----753f3ec04ba1-----------------------------------)

[Homepage](https://medium.com/?source=post_page-----753f3ec04ba1-----------------------------------)

[![Towards Data Science](https://miro.medium.com/max/224/1*AGyTPCaRzVqL77kFwUwHKg.png)](http://towardsdatascience.com/?source=post_page-----753f3ec04ba1-----------------------------------)

[Sign in](https://medium.com/m/signin?operation=login&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fwhy-you-should-try-rclone-with-google-drive-and-colab-753f3ec04ba1&source=post_page-----753f3ec04ba1---------------------nav_reg--------------)

[Get started](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fwhy-you-should-try-rclone-with-google-drive-and-colab-753f3ec04ba1&source=post_page-----753f3ec04ba1---------------------nav_reg--------------)

[Homepage](https://medium.com/?source=post_page-----753f3ec04ba1-----------------------------------)

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fcollection%2Ftowards-data-science&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fwhy-you-should-try-rclone-with-google-drive-and-colab-753f3ec04ba1&collection=Towards+Data+Science&collectionId=7f60cf5620c9&source=post_page-----753f3ec04ba1---------------------follow_header--------------)

[602K Followers](http://towardsdatascience.com/followers?source=post_page-----753f3ec04ba1-----------------------------------)

·

[Editors' Picks](https://towardsdatascience.com/tagged/editors-pick?source=post_page-----753f3ec04ba1-----------------------------------)[Features](https://towardsdatascience.com/tagged/tds-features?source=post_page-----753f3ec04ba1-----------------------------------)[Deep Dives](https://towardsdatascience.com/tagged/deep-dives?source=post_page-----753f3ec04ba1-----------------------------------)[Grow](http://towardsdatascience.com/how-to-get-the-most-out-of-towards-data-science-3bf37f75a345?source=post_page-----753f3ec04ba1-----------------------------------)[Contribute](http://towardsdatascience.com/questions-96667b06af5?source=post_page-----753f3ec04ba1-----------------------------------)

[About](http://towardsdatascience.com/about?source=post_page-----753f3ec04ba1-----------------------------------)

[Get started](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fwhy-you-should-try-rclone-with-google-drive-and-colab-753f3ec04ba1&source=post_page-----753f3ec04ba1---------------------nav_reg--------------)

[Open in app](https://rsci.app.link/?%24canonical_url=https%3A%2F%2Fmedium.com%2Fp%2F753f3ec04ba1&%7Efeature=LoOpenInAppButton&%7Echannel=ShowPostUnderCollection&%7Estage=mobileNavBar&source=post_page-----753f3ec04ba1-----------------------------------)

[Homepage](https://medium.com/?source=post_page-----753f3ec04ba1-----------------------------------)

# Why You Should Try Rclone with Google Drive and Colab

## Wouldn’t it be nice if you never lost your trained ML models on the Google Colab? Rclone to the rescue.

[![Steven Smiley](https://miro.medium.com/fit/c/56/56/1*SFh1G75eur9Ap-P9nR1t4g@2x.jpeg)](https://stevensmiley1989.medium.com/?source=post_page-----753f3ec04ba1-----------------------------------)

[Steven Smiley](https://stevensmiley1989.medium.com/?source=post_page-----753f3ec04ba1-----------------------------------)

[Jun 17·4 min read](http://towardsdatascience.com/why-you-should-try-rclone-with-google-drive-and-colab-753f3ec04ba1?source=post_page-----753f3ec04ba1-----------------------------------)

![](https://miro.medium.com/max/1400/1*zwuyyUli5m3oLPujMLjeBw.jpeg)

Image by author.

Do you ever start training a machine learning model on the Google Colab and the runtime disconnects before you can save your results? It use to happen to me and I would get frustrated. I would leave my model training to come back a few hours later and find it finished without saving!

![](https://miro.medium.com/max/1136/1*RU16B34oOhM4AZe-b-yhjw.png)

Image by author.

_So what can you do about this? Use Rclone¹, Google Drive², and Google Colab³ together with the following 3 major steps:_

**_1) Install Rclone._**

**_2) Configure Rclone._**

**_3) Export with Rclone._**

# **Step 1. Install Rclone.**

Do this in the very first cell of your Google Colab Jupyter Notebook.

```
<span id="3c3b" class="hr mn lk gu mo b dn mp mq s mr">! curl https://rclone.org/install.sh | sudo bash</span>
```

# Step 2. Configure Rclone.

Configure the newly installed Rclone.

```
<span id="ff6d" class="hr mn lk gu mo b dn mp mq s mr">!rclone config</span>
```

## **Step 2.1. Make a new remote**

![](https://miro.medium.com/max/60/1*E6fODE39kJFirsPqsJvBbA.png?q=20)

## Step 2.2. Name it “remote”

![](https://miro.medium.com/max/60/1*8v7tzEs9uoG8qa_w0LMHow.png?q=20)

## Step 2.3. Enter “15” for the Google Drive

![](https://miro.medium.com/max/40/1*UuMLvXx0DS4-0WuU-1YWsw.png?q=20)

## Step 2.4. Press Enter for default on client\_id

![](https://miro.medium.com/max/60/1*h-P-IsvVp2Fajo188pV2YQ.png?q=20)

## Step 2.5. Press Enter for default on client\_secret

![](https://miro.medium.com/max/60/1*HUKMVARtHJDw7Hyw7qgHRg.png?q=20)

## Step 2.6. Enter “1” for Full access all files on your Google Drive.

![](https://miro.medium.com/max/60/1*3xhN6IP5qw9ZcpDo4kZgIg.png?q=20)

## Step 2.7. Press Enter for default on root\_folder\_id.

![](https://miro.medium.com/max/60/1*LYFEG-cK-n50mbGVIFWVHw.png?q=20)

## Step 2.8. Press Enter for default on service\_account\_file.

![](https://miro.medium.com/max/60/1*upuKdv5QohpC68bWHD1FvA.png?q=20)

## Step 2.9. Enter “n” for default on advanced config.

![](https://miro.medium.com/max/60/1*tNgOBU-4wJCO0BrrzlA5kA.png?q=20)

## Step 2.10. Enter “n” for non-default on Remote config.

![](https://miro.medium.com/max/60/1*Ibo9Ozwh4_Q_na3jeaqhAw.png?q=20)

Go to the link it generates for you.

![](https://miro.medium.com/max/60/1*WXNXI_QYgSA0vcLbh67hxg.png?q=20)

Copy the code from your Google Drive Sign in for Rclone access.

![](https://miro.medium.com/max/60/1*v6nvs8Acs1Z3MeWyQsGVlw.png?q=20)

Paste it where it tells you to Enter verification code

![](https://miro.medium.com/max/60/1*gz09Z9FWuOWUwZZjk4zgDg.png?q=20)

## Step 2.11. Enter “n” for default on Shared Drive.

![](https://miro.medium.com/max/60/1*-Lz2k5MCnNhkO39oiq1ItQ.png?q=20)

## Step 2.12. Enter “y” for default on remote settings.

![](https://miro.medium.com/max/60/1*aklQf3aXlNB5uUtC6aQ4IA.png?q=20)

## Step 2.13. Enter “q” for Quit config.

![](https://miro.medium.com/max/60/1*30KqOaACQ9ZU_JCd0zZdzQ.png?q=20)

# Step 3. Export with Rclone.

Add an export after your model finishes training.

Copy your current “/content/” directory in the Google Colab to wherever you want on your Google Drive through the Rclone remote path we just established.

```
<span id="ebce" class="hr mn lk gu mo b dn mp mq s mr">!rclone copy "/content/"  remote:"/YOUR_PATH_TO_GDRIVE_DESIRED_LOCATION/"</span>
```

# Summary

So after following those 3 major steps outlined above, you should be able to back-up whatever models you are training with Google Colab (assuming they finish).

Here is an example [Jupyter Notebook](https://nbviewer.jupyter.org/github/stevensmiley1989/TensorFlow_Examples/blob/main/TF_TimeSeries_Custom_TFDataset/TF_TimeSeries_Custom_TFDataset.ipynb) that implements theses steps from start to finish.

You can see for that example, my Google Drive stored the trained models as such under _content_:

![](https://miro.medium.com/max/1400/1*0tPQnY9SkT5gA0P2pzChUA.png)

Image by author.

You can find more examples in this [Github repository](https://github.com/stevensmiley1989/TensorFlow_Examples) I made for various TensorFlow machine learning problem notebooks.

I hope you found this article helpful! Thank you for reading and hit the like if so. Follow me on here for more machine learning based content coming soon!

You can also follow me on LinkedIn: [https://www.linkedin.com/in/stevensmiley1989/](https://www.linkedin.com/in/stevensmiley1989/)

# References

1. Rclone.[ [https://rclone.org/](https://rclone.org/)]
2. Google Drive. [ [https://g.co/kgs/qu7aAY](https://g.co/kgs/qu7aAY)]
3. Google Colab. [ [https://colab.research.google.com/](https://colab.research.google.com/)]
4. TensorFlow. Martín Abadi, Ashish Agarwal, Paul Barham, Eugene Brevdo, Zhifeng Chen, Craig Citro, Greg S. Corrado, Andy Davis,Jeffrey Dean, Matthieu Devin, Sanjay Ghemawat, Ian Goodfellow, Andrew Harp, Geoffrey Irving, Michael Isard, Rafal Jozefowicz, Yangqing Jia,Lukasz Kaiser, Manjunath Kudlur, Josh Levenberg, Dan Mané, Mike Schuster,Rajat Monga, Sherry Moore, Derek Murray, Chris Olah, Jonathon Shlens,Benoit Steiner, Ilya Sutskever, Kunal Talwar, Paul Tucker,Vincent Vanhoucke, Vijay Vasudevan, Fernanda Viégas,Oriol Vinyals, Pete Warden, Martin Wattenberg, Martin Wicke,Yuan Yu, and Xiaoqiang Zheng. TensorFlow: Large-scale machine learning on heterogeneous systems, 2015. Software available from[tensorflow.org](http://tensorflow.org).

[**Steven Smiley**](https://stevensmiley1989.medium.com/?source=post_sidebar--------------------------post_sidebar--------------)

Writing about Data Science, CV, DL, ML, AI, Python [https://www.linkedin.com/in/stevensmiley1989/](https://www.linkedin.com/in/stevensmiley1989/)

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Fb3b698e2f8f1%2F753f3ec04ba1&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fwhy-you-should-try-rclone-with-google-drive-and-colab-753f3ec04ba1&user=Steven+Smiley&userId=b3b698e2f8f1&source=post_sidebar-b3b698e2f8f1----753f3ec04ba1---------------------follow_sidebar--------------)

45

45

45

- [Machine Learning](http://towardsdatascience.com/tagged/machine-learning)
- [Google Colab](http://towardsdatascience.com/tagged/google-colab)
- [Rclone](http://towardsdatascience.com/tagged/rclone)
- [Deep Learning](http://towardsdatascience.com/tagged/deep-learning)
- [Artificial Intelligence](http://towardsdatascience.com/tagged/artificial-intelligence)

## [More from Towards Data Science](https://towardsdatascience.com/?source=follow_footer-----753f3ec04ba1-----------------------------------)

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fcollection%2Ftowards-data-science%2F753f3ec04ba1&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fwhy-you-should-try-rclone-with-google-drive-and-colab-753f3ec04ba1&collection=Towards+Data+Science&collectionId=7f60cf5620c9&source=follow_footer-----753f3ec04ba1---------------------follow_footer--------------)

Your home for data science. A Medium publication sharing concepts, ideas and codes.

[Read more from Towards Data Science](https://towardsdatascience.com/?source=follow_footer-----753f3ec04ba1-----------------------------------)

## More From Medium

## [Automatic Video Editing using Python](http://towardsdatascience.com/automatic-video-editing-using-python-324e5efd7eba?source=post_internal_links---------0-------------------------------)

[Dmytro Nikolaiev (Dimid)](https://medium.com/@andimid?source=post_internal_links---------0-------------------------------)in [Towards Data Science](https://towardsdatascience.com/?source=post_internal_links---------0-------------------------------)

[![](https://miro.medium.com/max/60/1*LetzUw2pVvoi9jRLkBJcNA.jpeg?q=20)](http://towardsdatascience.com/automatic-video-editing-using-python-324e5efd7eba?source=post_internal_links---------0-------------------------------)

## [Big Data will First Slow, Not Accelerate, Discovery](https://medium.com/@eric_luellen/big-data-will-slow-not-accelerate-discovery-709b8e46b6e9?source=post_internal_links---------1-------------------------------)

[Eric Luellen](https://medium.com/@eric_luellen?source=post_internal_links---------1-------------------------------)

[![](https://miro.medium.com/max/60/1*hn4v1tCaJy7cWMyb0bpNpQ.png?q=20)](https://medium.com/@eric_luellen/big-data-will-slow-not-accelerate-discovery-709b8e46b6e9?source=post_internal_links---------1-------------------------------)

## [the least among high-income developed nations at 4.3%](https://allsportslivenow.medium.com/the-least-among-high-income-developed-nations-at-4-3-6df0acb8c6cb?source=post_internal_links---------2-------------------------------)

[Allsportslivenow](https://allsportslivenow.medium.com/?source=post_internal_links---------2-------------------------------)

[![](https://miro.medium.com/max/60/0*xkZAs0BGATjHNzkP.jpeg?q=20)](https://allsportslivenow.medium.com/the-least-among-high-income-developed-nations-at-4-3-6df0acb8c6cb?source=post_internal_links---------2-------------------------------)

## [What is true impact?](https://medium.com/logistimo/what-is-true-impact-b187e9f5a3e0?source=post_internal_links---------3-------------------------------)

[Arun Ramanujapuram](https://medium.com/@arun_94206?source=post_internal_links---------3-------------------------------)in [logistimo](https://medium.com/logistimo?source=post_internal_links---------3-------------------------------)

[![](https://miro.medium.com/max/60/1*cbR0xzpGAzoP2yuL_Fjbqg.jpeg?q=20)](https://medium.com/logistimo/what-is-true-impact-b187e9f5a3e0?source=post_internal_links---------3-------------------------------)

## [Visualization and Multiple imputation](https://rabkumarisinghisikolkata.medium.com/visualization-and-multiple-imputation-734b9e73f2b2?source=post_internal_links---------4-------------------------------)

[Rabi Kumar Singh](https://rabkumarisinghisikolkata.medium.com/?source=post_internal_links---------4-------------------------------)

[![](https://miro.medium.com/max/60/1*rd-p68WwLI95RGUMLH33yA.png?q=20)](https://rabkumarisinghisikolkata.medium.com/visualization-and-multiple-imputation-734b9e73f2b2?source=post_internal_links---------4-------------------------------)

## [Exploring Greater Sydney suburbs](http://towardsdatascience.com/exploring-greater-sydney-suburbs-f2bf1562988e?source=post_internal_links---------5-------------------------------)

[Tariq Munir](https://medium.com/@muneer.t?source=post_internal_links---------5-------------------------------)in [Towards Data Science](https://towardsdatascience.com/?source=post_internal_links---------5-------------------------------)

[![](https://miro.medium.com/max/60/0*u_ujB0gigJ7FfYnL?q=20)](http://towardsdatascience.com/exploring-greater-sydney-suburbs-f2bf1562988e?source=post_internal_links---------5-------------------------------)

## [A Brief insight on Data Pre-processing and Visualization for Machine Learning Model](https://medium.com/@suhanaanjum666/a-brief-insight-on-data-pre-processing-and-visualization-for-machine-learning-model-f3e2626506a0?source=post_internal_links---------6-------------------------------)

[Suhana Anjum](https://medium.com/@suhanaanjum666?source=post_internal_links---------6-------------------------------)

[![](https://miro.medium.com/max/60/1*hn4v1tCaJy7cWMyb0bpNpQ.png?q=20)](https://medium.com/@suhanaanjum666/a-brief-insight-on-data-pre-processing-and-visualization-for-machine-learning-model-f3e2626506a0?source=post_internal_links---------6-------------------------------)

## [Stack Index 📇](https://medium.com/featurepreneur/stack-index-45499406d84d?source=post_internal_links---------7-------------------------------)

[Vaishnavi V](https://vaishnavivenkat26.medium.com/?source=post_internal_links---------7-------------------------------)in [featurepreneur](https://medium.com/featurepreneur?source=post_internal_links---------7-------------------------------)

[![](https://miro.medium.com/max/60/1*us-7un5PgnZSzFrS6mhxvQ.jpeg?q=20)](https://medium.com/featurepreneur/stack-index-45499406d84d?source=post_internal_links---------7-------------------------------)

