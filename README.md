# Recommendation model using cosine similarity

In this project I will develop a model that will be able to recommend job’s advertisement based on a certain CV. I could divide the project into three parts:
1.	Scraping Data using Selenium and Beautiful soup.
2.	Developing the recommendation model using Cosine Similarity
3.	Sending emails attached the links of the recommended jobs
So let’s start with the first step and analyse the scraping process.

In order to create a job’s recommendation model we need a web page that could provide to us the essential data. The page that I picked for this step is the Indeed platform, I would like to emphasize that the whole process is for educational reasons with all the respect to companies and data. In addition, you can skip this step and just download some data samples that I saved above the readme section and jump to the Machine learning step.
Firstly, exporting the libraries that we are going to use:

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104214468-24626380-5440-11eb-85f8-5eca10908df7.png)

I am notgoing to dive in depth to describe the library’s functionality. I did it in apreview repository, you can find it in my profile with the name “Develop operationstrategy based on LinkedIn Data”. 
The second step is to create a function which will take two inputs, the job title and the area that we are looking for open positions. Writing now the documentation I noticed that we can scrape the Indeed page using only the Beautiful Soup library because it's a static page, on the other hand you can open the page using the Selenium module and find the searching boxes, write your query and click search by inspecting the right page elements. Definitely, you can try to do with your approach.  

![Χωρίς τίτλο](https://user-images.githubusercontent.com/66875726/104217126-a738ed80-5443-11eb-9530-4be255177cb6.png)



