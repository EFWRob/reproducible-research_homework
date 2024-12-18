# Reproducible research: version control and R

Question 4a.
Both walks start in the same initial location, but instantly diverge and cover markedly different areas. This is because with every step, or increment, the following increment will be at a random angle between 0 and 2π to the preceding increment, and independent of that preceding increment. From this it follows that the path taken is non-continuous.

Question 4b.
A random seed is an initial value (any random number) that algorithms use to produce sequences of seemingly random numbers. These PSNG (pseudorandom number generators) algorithms produce the same string of numbers corresponding to each seed number. This is the result of trying to model randomness using deterministic machines (computers), but also ensures reproducibility as the same algorithm with the same seed will always produce the same randomness. 

Question 4d
<img width="468" alt="Code_Changes" src="https://github.com/user-attachments/assets/9d5155fb-8814-4efc-9067-f7f088a51827" />

Question 5a
33 rows and 13 collumns

Question 5b
A log transform using the following code:
virion_data <- read.csv("Cui_etal2014.csv") 
virion_data_log <- virion_data %>%
  mutate(Log_Genome_length = log(Genome.length..kb.),
         Log_Virion_volume = log(Virion.volume..nm.nm.nm.))

Question 5c
Estimated α (Scaling Factor): 1181.807 , P value: 2.279645e-10
Estimated β (Exponent): 1.515228, P value: 6.438498e-10 
These are the same (accounting for the paper rounding) as the 2014 paper.

Question 5d

virion_data <- read.csv("Cui_etal2014.csv")

virion_data_log <- virion_data %>%
  mutate(Log_Genome_length = log(Genome.length..kb.),
         Log_Virion_volume = log(Virion.volume..nm.nm.nm.))

Virion_plot <- lm(Log_Virion_volume ~ Log_Genome_length, data = virus_data_log)

ggplot(virion_data_log, aes(x = Log_Genome_length, y = Log_Virion_volume)) +
  geom_point(color = "blue", size = 3) +  # Scatter points
  geom_smooth(method = "lm", color = "red", se = TRUE) +  # Regression line with confidence interval
  labs(
    title = "Log-Log Relationship Between Genome Length and Virion Volume",
    x = "Log(Genome Length)",
    y = "Log(Virion Volume)"
  ) +
  theme_minimal()

Question 5e
235306564197 nm³

## Instructions

The homework for this Computer skills practical is divided into 5 questions for a total of 100 points. First, fork this repo and make sure your fork is made **Public** for marking. Answers should be added to the # INSERT ANSWERS HERE # section above in the **README.md** file of your forked repository.

Questions 1, 2 and 3 should be answered in the **README.md** file of the `logistic_growth` repo that you forked during the practical. To answer those questions here, simply include a link to your logistic_growth repo.

**Submission**: Please submit a single **PDF** file with your candidate number (and no other identifying information), and a link to your fork of the `reproducible-research_homework` repo with the completed answers (also make sure that your username has been anonymised). All answers should be on the `main` branch.

## Assignment questions 

1) (**10 points**) Annotate the **README.md** file in your `logistic_growth` repo with more detailed information about the analysis. Add a section on the results and include the estimates for $N_0$, $r$ and $K$ (mention which *.csv file you used).
   
2) (**10 points**) Use your estimates of $N_0$ and $r$ to calculate the population size at $t$ = 4980 min, assuming that the population grows exponentially. How does it compare to the population size predicted under logistic growth? 

3) (**20 points**) Add an R script to your repository that makes a graph comparing the exponential and logistic growth curves (using the same parameter estimates you found). Upload this graph to your repo and include it in the **README.md** file so it can be viewed in the repo homepage.
   
4) (**30 points**) Sometimes we are interested in modelling a process that involves randomness. A good example is Brownian motion. We will explore how to simulate a random process in a way that it is reproducible:

   a) A script for simulating a random_walk is provided in the `question-4-code` folder of this repo. Execute the code to produce the paths of two random walks. What do you observe? (10 points) \
   b) Investigate the term **random seeds**. What is a random seed and how does it work? (5 points) \
   c) Edit the script to make a reproducible simulation of Brownian motion. Commit the file and push it to your forked `reproducible-research_homework` repo. (10 points) \
   d) Go to your commit history and click on the latest commit. Show the edit you made to the code in the comparison view (add this image to the **README.md** of the fork). (5 points) 

5) (**30 points**) In 2014, Cui, Schlub and Holmes published an article in the *Journal of Virology* (doi: https://doi.org/10.1128/jvi.00362-14) showing that the size of viral particles, more specifically their volume, could be predicted from their genome size (length). They found that this relationship can be modelled using an allometric equation of the form **$`V = \alpha L^{\beta}`$**, where $`V`$ is the virion volume in nm<sup>3</sup> and $`L`$ is the genome length in nucleotides.

   a) Import the data for double-stranded DNA (dsDNA) viruses taken from the Supplementary Materials of the original paper into Posit Cloud (the csv file is in the `question-5-data` folder). How many rows and columns does the table have? (3 points)\
   b) What transformation can you use to fit a linear model to the data? Apply the transformation. (3 points) \
   c) Find the exponent ($\beta$) and scaling factor ($\alpha$) of the allometric law for dsDNA viruses and write the p-values from the model you obtained, are they statistically significant? Compare the values you found to those shown in **Table 2** of the paper, did you find the same values? (10 points) \
   d) Write the code to reproduce the figure shown below. (10 points) 

  <p align="center">
     <img src="https://github.com/josegabrielnb/reproducible-research_homework/blob/main/question-5-data/allometric_scaling.png" width="600" height="500">
  </p>

  e) What is the estimated volume of a 300 kb dsDNA virus? (4 points) 
