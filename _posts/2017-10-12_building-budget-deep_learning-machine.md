

It all started when I was introduced into machine learning during a AI competition. As my old Macbook Air was running scalding hot training word embeddings, the provided Azure GPU service ended (the service was provided by the competition host and only lasted for 3 days). Finally, I decided to get myself a new desktop machine for deep learning purpose. The usual recommendation i found online was usually going for an i5 / i7, a GTX 1070 with a fairly large SSD paired with HDD. However, i decided to go for an abnormal approach with a slow CPU and more GPUs which may allow me to cover more “grounds” in a faster pace.

## **CPU+GPUs**

As recommended by [Tim Dettmers articles](http://timdettmers.com/2017/04/09/which-gpu-for-deep-learning/), more slower GPUs are more useful than a single powerful GPU. This is very useful when you are testing a new models while you are running another training session. You certainly don’t want to wait for hours on the CPU to train the new models on a small data batch. Hence, I decided to** spend most of my budget on GPUs while skimp on the CPU and other parts**. While this strategy sounds pretty brilliant, there’s some limitation on it which I will explain in conclusion.

![[https://imgflip.com/memegenerator/The-Most-Interesting-Man-In-The-World](https://imgflip.com/memegenerator/The-Most-Interesting-Man-In-The-World)](https://cdn-images-1.medium.com/max/2000/1*Fg23f-36OEAdIbsFuqPDrw.jpeg)*[https://imgflip.com/memegenerator/The-Most-Interesting-Man-In-The-World](https://imgflip.com/memegenerator/The-Most-Interesting-Man-In-The-World)*

## Under 1000 USD budget

Since I needed a motherboard to with two PCIe x16 in order to fit two GPUs while not spending too much money on motherboard. I decided to go with **Asrock B250m Pro4 **with two PCIex16 slots, 6 SATA port, two pcie SSD slots which cost about 85 USD. For SSD, I decided to go for **128G Western Digital SSD** paired with** 1+2TB two Toshiba HDD. **Thats 190 USD in total for storage. The 1TB hard disk was dedicated for Windows 10 since I was an electrical engineering undergrad, some course still required Window environment to finish the homework(Zzzz). RAM wise, I went for **16GB( 8GBx2) of DDR4 RAM** which cost me about 130 USD. For power supply I found a **Silverstone 600W** power supply under discount for only 52 USD.

### CPU and was refused to sell me GPU

For CPU I choosen **Pentium G4600** because of having 4 threads in a dual cores. This setup is quite questionable as my local provider started to question if I was doing crypto mining when I told them I wanted a GTX 1060 as well. In the end, they refused to sell me the GTX 1060 because of the ban to sell GPU to miners. Crap. ( Btw the CPU cost about 60 USD)

### **Finding GPUs**

Things only get worst when Etherium price was soaring like a rocket creating a GPU shortage on GTX 1060, GTX 1070. I had no choice but to buy a overpriced **4GB** **GTX 1050Ti** overclocked version from Galax for 165 USD. This card performance was nearly on par with GTX 1060 base clock only with lesser VRAM. VRAM is extremely important in deep learning as the VRAM basically limits how large the model can be and the batch size of each iteration during gradient descent. In short, small memory equals to smaller models and longer training time.

A few months later I get managed to buy the **Galax GTX 1060 6GB version **online for 250 USD. The local store still refused to sell me the 1060 despite my explain for deep learning use. As the time of this writing, there’s a rise on GPU price due to VRAM shortage. Hence, prepared for some expensive GPU when you are choosing.

## Performance and final notes

In the end, I spent a total of roughly 990 USD on my machines. Due to the dual GPU and a weak CPU setup, the system crash under heavy load when two models was under training process simultaneously. The cause of this problems came from the rather small RAM size and only two actual physical cores. Luckily the motherboard had two more RAM slots which allows me to expand in the future.

### Learn to Work with Limitation

When it comes to CPU heavy task, I have to move the task to a cloud instance with lots of CPU cores and huge RAM for computing. The results was later transferred back to my machine for further use. The two GPUs setup was proven to be the right choice as I could easily work with other neural network structure while the other neural networks was undergoing training process. The only drawbacks of 16GB RAM was I need to keep an eye on the RAM usage very close to ensure it was not overflowed.

Despite having a GTX 1060, when it comes to Kaggle competition, large datasets and a huge classification problems still requires powerful GPU to train your models. To overcome this problem, I started by writing the full code and undergo complete testing using smaller dataset on my GPUs before pushing the final code to the cloud for the long training process.

Recently, I started tinkering with model parallelism and data parallelism in Tensorflow. Having two GPUs again, was proven to be the right choice.

### Regrets

I came into realised choosing 120G of SSD wasn’t a good choice and wished I had choosen a larger SSD. When I partake in Kaggle Discount competition, the image dataset was too huge to fit into my RAM (58GB vs 16GB). During the training process, random accessing the database wasn’t an option as my SSD was nearly full. As shown in [tomshardware benchmark](http://www.tomshardware.com/reviews/ssd-upgrade-hdd-performance,3023-6.html) in CrystalDiskMark, the hard disk with 4kB random blocks were only 1.6 MB/s, while the SSD writes at 19.7 MB/s and reads at 70.6 MB/s. A nearly 70 times improvement over read speed.

## TLDR;

1. Choosing multiple “weaker” GPUs is better than a single powerful GPU

1. Do not choosen GPU other than the latest 10th generation Nvidia GPU due to much higher clock speed.

1. SSD should at least 240G and above

1. Choose CPU with more than 2 physical cores ( Coffelake i3 has 4 physical cores, which is more suitable for this budget build)

1. Power supply with 600W or above gives you more room for future upgrade.

