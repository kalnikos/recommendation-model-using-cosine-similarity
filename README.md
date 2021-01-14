# Recommendation model using cosine similarity

In this project I will develop a model that will be able to recommend job advertisements based on a certain CV. I will divide the project into three parts:
1.	Scraping Data using Selenium and Beautiful soup.
2.	Developing the recommendation model using Cosine Similarity
3.	Sending emails by attaching the links of the recommended jobs

So, let’s start with the first step and analyse the scraping process.

In order to create a job recommendation model we need a web page which provides us with the essential data. The page that I picked for this step is the Indeed platform. I would like to emphasize that the whole process is for educational reasons with all the respect to companies and the Indeed platform. In addition, you can skip this step and just download some data samples that I saved above the readme section and jump to the Machine learning step.
Firstly, exporting the libraries that we are going to use:

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104214468-24626380-5440-11eb-85f8-5eca10908df7.png)

I will not dive in depth to describe the librarys' functionality. I did it in a previous repository and you can find it in my profile with the name “Develop operation strategy based on LinkedIn Data”. 
The second step is about creating a function which will take two inputs, the job title and the area that we are looking for open positions. Writing now the documentation I noticed that we can scrape the Indeed page using only the Beautiful Soup library because Indeed is a static page. On the other hand, you can open the page using the Selenium module and find the searching boxes, write your query and click search by inspecting the right page elements. We can definitely scrape the page with many different  approaches.  

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104217126-a738ed80-5443-11eb-9530-4be255177cb6.png)

Using the Beautiful Soup module on this page and changing keywords in the URL you can inspect different results by using a simple function as the above. Notice that I am also using the time module in order to give some time to the browser to load the page properly. The page that we will scrape is this one:

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104219389-b8372e00-5446-11eb-831f-da7db7576f1c.png)

As we can see it is a page with boxes that include information about the position. So, we need these information plus the full job description to use it to compare it with certain CVs in the Machine learning process. The page loaded and now we will be able to parse the HTML content and start building a scrape function with the elements that we need. It iss worth checking at this stage if everything works properly. We can inspect this by printing the length of the list that contains the different job ads.

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104220832-bff7d200-5448-11eb-9c62-db5f89839b52.png)  

Till now everything looks working fine. Let’s see the parsing function and analyse some parts:

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104222452-fc2c3200-544a-11eb-9378-65aec5180207.png)

In the feature extraction process always consider finding a big elements which will make the process smooth. For instance, in this example I found the class which contains all the positions' ads; my next step was to isolate the first card and take the following features: job title, job URL etc. Using this approach I implement the function to every card on each searching page.  
After creating the function we can use it for all the available pages that we want to extract data and we may also determine the number of the outcomes. The other tricky part of this process is getting to the next searching page, I suppose and definitely, there are many methods that you can try. The method that I used is to find the next button at the bottom of the page and extract the element which contains the HREF of the next page. To get in to the next page you just have to combine the HREF with indeed main URL like the code bellow:

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104459491-77a9f280-55b5-11eb-96fa-067c0e69f2f6.png)

After the scraping is done you can convert the list to a csv file and start analysing the data. In my case I ran the scraping script a few more times in order to parse different available open positions and create a dataset that will help me to develop the recommendation model.

## Recommend open positions based on a particular CV 

Assume that we are running an operation where the documents are so many and you don’t have much time to read everything or you are just trying to sort your documents and categorize them in different folders. Definitely time consuming tasks, but not anymore, using tools like Algebra and our computer we can find a technique to do it quickly. I will use the Cosine Similarity method for my recommendation model but first let me explain why and How it works.

Cosine Similarity is a method for determining how similar two documents are. Certainly there are many more methods that you can use for finding the text similarity but Cosine is irrespective of the document size. I mention size because one way to find the similarity is by counting the words of a sentence compared to another and if they are having many common words we assume that they are similar. Not so quickly, what’s happening if the texts that we are comparing are having different sizes, the longer the text more words to count that may lead to inaccurate result.

For instance:

Text 1: I love ice cream
Text 2: I like ice cream
Text 3: I offer an ice cream to the lady that I love

Let’s compare the texts by counting the common words

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104487882-50afe880-55d6-11eb-9ef2-7bdc479a0446.png)

Text 1 – Text 2: 3 common words
Text 1 – Text 3: 4 common words
Text 2 – Text 3: 3 common words

So according to the results the text 1 is more similar to the text 3 which in fact is not true.


We have the same issue using the Euclidean Distance the length is a factor that adversely affects the outcome according to the equation that calculate the distance:

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104490092-17c54300-55d9-11eb-930e-68cd2f5974cb.png)

Text 1: I love football
Text 2: I love playing and watching football
Text 3: I hate football
The sentence 1 with the sentence 3 have the opposite meaning but after using the Euclidean equation the distance between sentence 1 and 3 will be shorter compared to the sentence 2, so again the length of the sentence affected the result.

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104495396-662a1000-55e0-11eb-9e4f-eb959b7522cb.png)

Big distance number means dissimilarity, but how could we define that number? How could we define a threshold of similarity considering that the distance could be a very big number.

We can overcome these issues by using the Cosine Similarity method. Cosine Similarity measures the cosine of the angle between two vectors in the space. In my case I am using words that appear in documents. Plotting the words in a multi-dimensional space where every dimension represents a word the Cosine Similarity represents the angle of the documents and not the magnitude aka (How many times the words appears on a document). If you want to find the magnitude you can use the Euclidean distance.
The Cosine Similarity isn't affected by length of the text and asymmetrical texts may have a smaller angle between them, smaller the angle higher the similarity.

The equation for computing the Cosine Similarity is this:

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104580371-dd55b780-5665-11eb-8cbf-511894044334.png)

Unfortunately, it’s not possible to plot an example when we are having more than three dimensions aka words. Despite that, I will use Python in order to represent how it words.

You can check the file that I posted above the read me section with the name “Cosine_similarity_example”. Let’s continue with the recommendation model.

Initially, I will create a data frame which will contain jobs from different sectors. Let's read those csv files and concatenate them into a data frame in order to develop the recommendation model.

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104584027-974f2280-566a-11eb-82d8-3f89469e5067.png)

The nextstep is to drop duplicates that our data set may have and read the CV that weuse for recommendation. In addition, We can do some text cleaning.

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104584553-70ddb700-566b-11eb-91c8-0df0c4b085db.png)

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104584943-0416ec80-566c-11eb-9349-aefe18567d62.png)

The goal isto create a model that will send available open positions to the person whosubmit the CV. We need the Job description and the URL from our data set and alsowe need to create a URL for every CV that we insert in our data set in order tocreate a discrete feature. 

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104586084-a8e5f980-566d-11eb-8c96-ecf26575edb0.png)

It is also usefulto download some NLP packages that can optimize the text manipulation process, hereis a link where you can find more detail about it: https://morioh.com/p/04a148fa2131

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104588261-c9638300-5670-11eb-8754-3033afe5465d.png)

We can apply the packages to our text column with some other essential manipulations by creating a function:

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104588800-95d52880-5671-11eb-88ab-46bd07d8931c.png)

The data set is ready for implementing the Cosine Similarity method.

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104589151-1dbb3280-5672-11eb-980b-b6acbf9cb02f.png)


![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104589309-522eee80-5672-11eb-8e08-2699b7617d26.png)

The nextstep is to find the index of the CV that we insert to the data set and returnthe most similar job descriptions. Sort the job descriptions in descendingorder and determining how many you want to save.

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104590050-6fb08800-5673-11eb-8eec-b47b21b45782.png)

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104590174-9cfd3600-5673-11eb-9609-70510bccfd45.png)

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104590288-c6b65d00-5673-11eb-9ff7-50319dab04a1.png)




