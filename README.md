# Recommendation model using cosine similarity

In this project I will develop a model that will be able to recommend job’s advertisement based on a certain CV. I could divide the project into three parts:
1.	Scraping Data using Selenium and Beautiful soup.
2.	Developing the recommendation model using Cosine Similarity
3.	Sending emails by attaching the links of the recommended jobs

So, let’s start with the first step and analyse the scraping process.

In order to create a job’s recommendation model we need a web page that could provide to us the essential data. The page that I picked for this step is the Indeed platform, I would like to emphasize that the whole process is for educational reasons with all the respect to companies and data. In addition, you can skip this step and just download some data samples that I saved above the readme section and jump to the Machine learning step.
Firstly, exporting the libraries that we are going to use:

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104214468-24626380-5440-11eb-85f8-5eca10908df7.png)

I will not dive in depth to describe the librarys' functionality. I did it in a preview repository, you can find it in my profile with the name “Develop operation strategy based on LinkedIn Data”. 
The second step is about creating a function which will take two inputs, the job title and the area that we are looking for open positions. Writing now the documentation I noticed that we can scrape the Indeed page using only the Beautiful Soup library because Indeed is a static page, on the other hand you can open the page using the Selenium module and find the searching boxes, write your query and click search by inspecting the right page elements. We can definitely scrape the page with many different  approaches.  

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104217126-a738ed80-5443-11eb-9530-4be255177cb6.png)

Using the Beautiful Soup module on this page and changing keywords in the URL you can inspect different results by using a simple function as the above. Notice that I am also using the time module in order to give some time to the browser to load the page properly. The page that we will scrape is this one:

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104219389-b8372e00-5446-11eb-831f-da7db7576f1c.png)

As we can see is a page with boxes that includes information about the position, So we need those information plus the full job description for using it to compare it with certain CV’s in the Machine learning process. The page has loaded and we could parse the HTML content and start building a scrape function with the elements that we need. It’s worth checking at this stage if everything works, in this page we can check this by printing the length of the list that contains the different job ads.

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104220832-bff7d200-5448-11eb-9c62-db5f89839b52.png)  

Till now everything looks that working fine, so let’s see the parsing function and analyse some parts:

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104222452-fc2c3200-544a-11eb-9378-65aec5180207.png)

So, in the feature extraction process always think that finding a big element will make the process smooth. For instance, in this example I found the class which contains all the position’s ads; my next step was to isolate the first card and take the above features: job title, job URL etc. Using this approach I could implement the function to every card on each searching page.  
After creating the function we can use it for all the available pages that we want to extract data and we may also determine the number of the outcomes. The other tricky part of this process is getting the next searching page I suppose, and definitely there are many methods that you can try. The method that I used is to find the next button at the bottom of the page and extract the element which contains the HREF of the next page. To get in to the next page you just have to combine the HREF with the indeed main URL like the code bellow:

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





