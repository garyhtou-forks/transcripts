**Daniel Whitenack:** Hello, and welcome to another Fully Connected episode of the Practical AI podcast. In these Fully Connected episodes Chris and I keep you connected with everything that's happening in the AI world, and hopefully share some resources with you to help you level up your machine learning game. My name is Daniel Whitenack, I am CEO and founder at Prediction Guard, where we're safeguarding private AI models, and I'm joined as always by Chris Benson, who is a principal AI research engineer at Lockheed Martin. How are you doing, Chris?

**Chris Benson:** Doing great today, Daniel. How are you?

**Daniel Whitenack:** I'm doing well. Yeah, yeah. Lots going on, lots of fun stuff in the AI world... But Chris, I have to say - so one of our listeners pointed out something which I realized afterwards as well, on our last Fully Connected episode, the one about GPT 4.0, or Omni, we played some clips of the voice assistant and we talked a little bit about the model. And the model, of course, was released, and we were using it... But the voice back and forth wasn't yet plugged into GPT 4.0. So they're just, I think, releasing that shortly. So I think there was a bit of general confusion in the community about -- because when you click that button, it's like you just take over into the voice interface, and it's like, I was on GPT 4.0, and so... I probably could have been maybe handled a bit better on our end, and maybe their end, too... But Open AI got us, I guess. We were fooled. \[laughs\] But yeah, still really cool stuff. Still, the things that we talked about are still what GPT 4.0 is, but just wanted to clarify that for our listeners if they had listened to that previous episode.

**Chris Benson:** While we're doing that, I realized I had made a mistake on that same issue after the show, that I wanted to confess on... I had watched all the videos over and over again, about the video portion doing that... And then when we were in the show, I had what I will claim as a senior moment where I was thinking just -- I watched so much of video I was thinking "Oh yeah, I did that." And so it wasn't... Afterwards, I was like "No, that was the videos I was watching. What was I thinking...?" So anyway, I wanted to confess. So we had a couple of blunders on that one, but having fun.

**Daniel Whitenack:** There you go. In our eagerness and excitement to talk about GPT 4.0 and record it very quickly afterwards, we got got. So...

**Chris Benson:** We both got got there, so all good. We'll move on. Well, for listeners who don't know, the show is fairly spontaneous, if you haven't been following us long... And we dive into stuff pretty quick. And occasionally, occasionally we fumble a little bit with that.

**Daniel Whitenack:** Yeah, yeah. So thanks for journeying with us through this wild and crazy world of AI. Now I think something that's been on my mind quite a bit, Chris, with some recent announcements, but also things that have been kind of developing over the past months is this area of local offline AI and AI PCs. They're sort of -- people are using this terminology AI PCs and --

**Chris Benson:** It's the current marketing hype.

**Daniel Whitenack:** Yeah, the current marketing hype... So I thought maybe we could dig into a little bit of that today and talk through kind of what exactly does that mean, how are people using AI models locally, what is an AI PC, what are the relevant kind of types of models and optimizations that can run locally... All of that seems to be a big -- well, it's a little bit hard to parse out some of that maybe if you're new to this space, and what is a GGUF versus Ollama, or all these things coming out... So yeah, I thought that would be good to dig into. And I know that you have been interested in kind of AI at the edge for some period of time... How do you see -- whether it's a staff laptop, or maybe a heavy compute node in a manufacturing plant or something, where you'd want to run AI "at the edge", or locally, let's say; generally locally, you're offline... What are the reasons that people would sort of want to go that direction?

**Chris Benson:** Well, this is kind of a thread we've talked about off and on on different episodes over time, and... You know, AI models are hosted in software, and they're going to always be wrapped in that. And software expands from the cloud all the way out into every device that we're already using, and so it's only natural that as AI becomes more accessible, and cheaper to deploy, that you're going to start having models that are kind of ramping up existing software out there. And there's of course, we're going through all the hype that's associated with that, but the way I see it is it's simply just a natural evolution of where software development would go.

\[05:45\] And to your point a moment ago about the hardware side - we don't talk about that a lot. We're very software-focused in general... But the hardware side is really going through a revolution. I know that in your business you have a partnership with Intel, and are seeing that in that capacity, and I certainly see that in my day job... And so there are so many more hardware capabilities coming out to support these functions, many of which are targeting low-power, disconnected environments... And so this is a timely topic. And if you look back for a precedent before that, we've always seen over the years in software and cloud development kind of a shifting back and forth between local capability, as suddenly you get a new generation of hardware and things will go a little bit more local, and you'll have your own equipment, and then things will move back into the cloud... And that natural give and take is part of the flow, and I think right now we've been so cloud-focused the last few years, because that was really the only available option, that now we're seeing a lot of new capability rolling out on both hardware and software models that are going to enable edge functionality to really explode over the next few years.

**Daniel Whitenack:** Yeah. I was asked -- I was at a conference last week, and I was asked which direction things would be going, either local AI models or hosted in the cloud... And I think the answer is definitely both, in the same way that there is a place for -- if you just think about databases, for example, as a technology, there's a place for embedded local databases, that operate where an application operates. There's a place for databases that run kind of at the edge, but on a heavier compute node that serves maybe some environment, and there's a use case for databases in the cloud. And sometimes those even coexisting, for various reasons.

In this case, we're talking about AI models. So I have a bunch of files on my laptop; I may not want those files to leave my laptop, so it might be privacy reasons that I want to search those files or ask questions of those files with an AI model. So privacy security type of thing, or in a healthcare environment they may have to be airgapped, or offline sort of thing, or public utilities sort of scenario, where you can't be connected to the public internet... But then it might just be also because of latency or performance, inconsistent networks, or flaky networks, where you have to operate sort of online/offline... There's a whole variety of reasons to do this. But yeah, there's also a lot of ways that, as you said, this is rapidly developing, and people are finding all of these various ways of running models at the edge. And we can highlight -- if you're just into this now, and getting into AI models, maybe you've used open AI's endpoint, or you've used an LLM API... If you wanted to run a large language model, or an AI model on your laptop, there's a variety of easy ways to do that. I know a lot of people that are using something like LLM Studio - this is just an application that you can run and test out different models...

There's a project called Ollama, which I think is really nice and really easy to use. You kind of just spin it up; you can either spin it up as a Python library, or as a kind of server that's running on your local machine, and interact with Ollama as you would kind of an LLM API. And then there's things like llama.cpp, and a bunch of other things. These I would kind of categorize as local model applications or systems where there's either a UI, or a server, or a Python client that's kind of geared specifically towards running these models locally.

And then there's a sort of whole set of technologies that are kind of Python libraries or optimization or compilation libraries that might take a model that's maybe bigger, or not suited to run in a local or lower-power environment, and run that locally.

\[10:03\] So if you're using the Transformers library from Hugging Face, you might use something like Bits and Bytes as a library to quantize models, shrink them down... There's optimization libraries like Optimum, and MLC, OpenVINO... These all have -- some exist for some period of time. Actually, I think in the past, we've had the Apache TVM project on the show, and we talked about OctoML... So this is not a new concept, because we've been sort of optimizing models for various hardwares for some time. But these optimization or compilation libraries are also usually kind of hardware-specific, so you optimize for a specific hardware. Whereas other of these local model systems are maybe more general-purpose, less optimized for hardware specifically. I don't know if you've got a chance to try out any of these systems, Chris, running some models on your laptop...

**Chris Benson:** I have, a little bit. I've used Ollama. I think that's my go-to.

**Daniel Whitenack:** And you have like an M1, or M2, M3, whatever M there is now, MacBook?

**Chris Benson:** Yeah, I have an M2. I have a couple of different laptops. One that's old, and one that's -- well, I guess an M2 is old by today's standards, so I may have to upgrade that one pretty soon... But yeah, I've used Ollama primarily. I probably haven't used as many of the tools as you have, given the business that you're in.

I think one of the things that I'm really interested as people are doing this now is understanding -- because we're really focusing on the infrastructure, the plumbing of making all this work locally, and doing the integrations with the cloud... But I think there's another thing just to throw into the mix of the conversation, and that is how, as people start, whether in the cloud, or particularly local, having multiple models out... And you have the infrastructure now, as we're talking about, to run it, that's starting to look at the API and the middleware to enable inferencing across APIs without direct human intervention, and have it make sense, where you have different responsibilities... Much like we have had for a number of years in the software realm. So as we're talking about that, I wanted to throw that in as another topic that I think is going to be really, really important, and hasn't had nearly as much attention as the fundamental infrastructure.

**Daniel Whitenack:** Yeah, I think that gets probably to a couple of things... One current major difference between sort of hosted cloud models and offerings versus local models is likely you're not going to run a mix of ten different LLMs on your local laptop, all at the same time, all loaded into memory. That would be, at least right now, a pretty significant ask to kind of switch between models in that way. But there are certainly cases where I think the market is showing that people want to not be restricted to one model family, and they're spreading out their usage against multiple models. So that definitely needs to happen in the cloud, and from model providers... But that doesn't mean you couldn't throw in the mix a selection of local models as well, for specific purposes...

And I think that gets to the other thing that you're talking about, which is kind of data integration, automation, pipelining, all of that sort of thing. I saw a comment on LinkedIn - I think it was even this morning - that those that are really winning in the AI space are those that have taken what they've learned kind of from automation, data pipelining, data integration in previous cycles of data science, and integrated those with generative models at various stages... Because a lot of the value - and I've seen this, too; a lot of the value that you get out of these models is not the models themselves, but the system that you build around them. And that involves a lot of data integration and automation, and maybe even routing between different models in the case that we're talking about here maybe even routing between local models and cloud models...

\[14:15\] And so yeah, I think that that's really stressed, especially as you talk about running these models kind of everywhere, quote-unquote, across cloud, and local, and on-prem, and data center environments. But yeah, it's interesting... I don't myself have an AI PC yet; maybe at some point I will, but... Yeah, I'm excited to see where all this goes.

**Chris Benson:** Indeed. As we push forward, I think one of the things that I'd like to see, especially for local -- you know, we mentioned a few minutes ago Ollama and some of the other tools for infrastructure... As we were talking here, I was looking through Yann LeCun's various posts, because he was proposing recently in the last week or two prior to this conversation kind of a way of structuring different model interactions, from a responsibility standpoint, that they're doing at Meta. Of course, at my employer, we have our own version of that, on how we structure different things... But really interested in seeing if the community kind of comes around with kind of an open framework, a best practice framework around how to do that. You know, be able to do it on a laptop, on an M2, M3, M4, be able to have those interactions locally, and a framework that would span between that local and the cloud interaction, so that you have something -- and I don't think that right now everyone seems to be doing that on their own. There's a lot of similarities between them, but there doesn't seem to be kind of a standard approach to how that all comes together.

**Break**: \[15:52\]

**Daniel Whitenack:** Well, Chris, there's an increasing number of options... If you were to explore this space and kind of that interaction of local models with your systems, there's an increasing number of choices of "AI PCs", which I think is a hyped term now... One of them - you mentioned Intel coming out with AI PCs. I think Lenovo is shipping some with the Intel's Core Ultra processor. I think the name is Meteor, the codename at least... And similar probably too as a response to maybe what's more familiar - I already mentioned the M1, M2, M3 etc. line from Apple... But Nvidia is also working hard on the GeForce RTX AI PCs, which - they've been kind of gaming PCs with GPUs in them for some time... But I think most of these "AI PCs" are more of an integrated type of processor or system where it's not just like an add-on to the laptop, but in the case of like the Core Ultra or the M2 there's actual processing in the architecture that is optimized for executing models. And so they're sort of AI-ready, shipping AI-ready.

And that brings up kind of some interesting questions in my mind, which are "Well, how do all these AI PCs compare?" If I'm about to get myself an AI PC, where should I go? And in thinking about that, and looking at some of these benchmarks, I was really encouraged to see that ML Commons, which is the organization behind MLPerf, which is a set of benchmarks and working groups that have been working for some time to benchmark various systems for performance on running AI workloads, machine learning workloads - they've just announced this spring an MLPerf Client Working Group, which is really geared towards essentially an application or a workload that you could run across these various AI PCs, or maybe AI-enabled edge machines, and that sort of thing, to really do kind of LLM-based workloads, and do some benchmarking for both training and inferencing on these "clients". So they're kind of referring to these generally as clients. So they say "The new ML Commons effort will build ML benchmarks for desktop, laptop and workstations for Microsoft's Windows and others operating systems." Quite interesting.

As far as I can tell, someone in our -- again, sometimes we get things wrong... So someone in our audience can correct us. Maybe David from ML Commons, who has been on the show before, he can correct us if something's already been published, but... I couldn't find this sort of set of benchmarks, so I think it's a work in progress. But really excited to see this when it comes out.

**Chris Benson:** Yeah, I think it'll be interesting as these laptops come out -- it's hard to imagine that the entire industry doesn't have to go full-in on this regardless, and thus kind of making the distinction of an AI laptop a little bit of a redundant thing... Because there's a point - and maybe we've already arrived now - where the idea of purchasing a new laptop that is not an AI laptop is a ridiculous thing. It becomes a must have feature to have going forward, and therefore all laptops kind of have to go that direction at some point here.

**Daniel Whitenack:** \[21:54\] Yeah. Well, I definitely think that could be one downside of this whole thing... I mean, I know the prices will go down, but these things are really expensive right now. So there is going to be a sort of disparity of those already for some period of time. If you're a new developer, maybe an indie developer, that purchase of that MacBook is a pretty significant expense for you already. And myself, I just use a refurbed ThinkPad from four years ago, not an AI PC. It's a Core i5. And you know, not a terrible laptop, but definitely not anything that anyone would necessarily be jealous of.

Now, I can run some models on this laptop, using Ollama and other systems, and I think that that gets down to maybe another element of this. So there's going to be, on one side, these clients that get increasingly sophisticated, and build in more AI-enabled or accelerating functionality into their chipset, and into their hardware... But there's also going to be increased sophistication on optimizing models that can't run locally, such that they can run locally. And this is where people might kind of -- I think this is also a point of common confusion that I've heard in workshops that I've given at conferences and other places, where people kind of look at - let's say it's LLaMA 3, or something like that. I wanna run LLaMA 3. Well, you go to Hugging Face, and the top downloaded LLaMA 3 is the base model. And then you've got these fine-tunes for instruction or chat. And then you've got all of these other flavors of LLaMA 3, like GGUF, GGML, QAT, AWQ... All sorts of acronyms that are really difficult to understand. So maybe it would help to just break this down just slightly.

Usually, when a model is released, they release a base model, or a pretrained model, or whatever it's called. A base model. So that's that kind of shortest name, usually. The Meta LLaMA 3. That usually is maybe a good model that you might findtune off of, but not generally the best model to start with, because it's a base model, it's not fine-tuned for any sort of set of general instruction following or chat... And they usually release along with that then a set of fine-tuned models for instruction or chat. So you've got LLaMA 3 Instruct, which is usually the better model... And then you've got this whole world of community members out there that build pipelines. So we had Nous Research on... They have pipelines built so that when a model is released, they can create all these different flavors of it, which include flavors for running these optimized in certain ways.

So these would be these other acronyms that we can dig into a little bit... But these are most of the time either additional fine-tunes, or quantized versions, or somehow optimized versions of these models that are meant to be run in kind of a diverse set of environments.

**Break**: \[25:26\]

**Daniel Whitenack:** Well, Chris, I kind of started getting into the alphabet soup a little bit... I don't know if you're sometimes as confused as I am with all of these model names...
**Chris Benson:** Often.

**Daniel Whitenack:** ...but they're getting increasingly long.

**Chris Benson:** Yes. Finish your point there, and then I have a question for you afterwards.

**Daniel Whitenack:** Yeah, yeah, sure. No, I was just gonna highlight a few of these different quantization methods, so that people can maybe have them in their mind... So there's the flavors that are GGML or GGUF; you might see those letters. This is GPT-Generated Unified Format. That's what that stands for. And this is an optimization of a model that will take that model that maybe requires a GPU to run that's larger, and creates a C++ replica of the LLM, and allows you to run it in quantized versions, meaning that the parameters of the model are taken from numbers that might have 32 or 16 digits behind the period, and get that down to two or four or eight, that sort of thing... Which makes the model smaller and more efficient. So these are mostly geared towards CPU or laptop kind of environments.

There's also GPTQ, which is really a focused kind of quantization method, but it's still meant for GPU only. So these usually ship in similar kind of formats to your previous models, but they do kind of some calibration-informed quantization to get that model smaller.

There's QAT, which is quantization-aware training, which as it might sound, involves some actual training, retraining of the model to inform the quantization... There's others like AQW, and this is another quantization method... So all of these sort of letters that you see, if you're wondering what those are - those are all kind of referring to these different kind of flavors of the model that might be generated for either running the model in an optimized way locally, on a CPU, on a laptop, or optimized still on a GPU, but in a smaller format that's more efficient.

**Chris Benson:** What are your thoughts on the CPU derivative? What are your thoughts on performance and capability relative to its own base model and its GPU siblings?

**Daniel Whitenack:** Yeah, I think that the reality right now, and then maybe where it's headed - I think the reality right now is the CPU-based models, even you can run some models that are even 7 billion parameters or something in some quantized version on a CPU. You're not going to get the same throughput as you would with hosting the model on a GPU, in other words the kind of tokens per second; the speed at which you're generating will be lower. But it's possible to run those.

What you're not going to do is - and this is what I also tell people... The same way that you're not going to host your microservice for your company on your laptop, you're not going to host some AI functionality for your company on your laptop, usually. That's going to still live in the cloud. But if you have some sort of private use case where something can't leave the laptop, or maybe you're deploying laptops in a disaster relief scenario, and there's going to be not that much connectivity... It's still enough throughput to get responses. So if you had chat over your disaster relief docs, and that on your laptop - it's still enough to get an answer in that scenario. And people can push it pretty far. I think the difference is just -- again, it's not one or the other, it's the use case, I guess.

**Chris Benson:** \[31:01\] Yeah. And just to add to that use case slightly. I think there's also disconnected or partially connected mobile platforms, where you can't necessarily rely on the cloud access, and you have devices that are out there as well, just to lump that in.

Kind of pulling around full circle for a moment back to the laptops, these AI laptops coming out... Kind of thinking back to the natural kind of segregation of responsibilities that we have in software development, aside from just the AI world, would you imagine that a reasonable level of support in those would be to be able to actually do training on like 7 billion-sized models, the smaller range... There's so much more of those, where maybe in the not so distant future I'm training a model, it's in that range, my own laptop can handle that, not just for inference, but for training... And then for very large models, that are still cloud-based, do you think that is a reasonable level that we might see AI laptops able to support?

**Daniel Whitenack:** I mean, I think that you can see some people trying some more training, or rather fine-tuning sorts of things on diverse hardware... I think basically what I'm seeing right now is still primarily inference on local machines, and utilization of things like in-context learning and RAG type workflows to integrate data, rather than fine-tuning locally. So I think that that's kind of the reality of where it is.

I think there's a possibility in the future maybe of some type of training type of scenarios that will happen, maybe not on client devices, but spread across client devices. It's been a while since we've talked about federated learning, but it will be interesting to see if that kind of rears its head in this world. I know that there's been efforts to kind of train LLM adapters in a federated way, and there's some papers about this, and share kind of parameter-efficient updates to weights across different client devices. That seems really intriguing to me.

But yeah, I don't know, we'll see where it goes. Maybe I'll be proved wrong, but I think I'm increasingly more of a proponent of most people don't need to fine-tune. A lot of it can be done with RAG, and chaining, and agents, and selecting the right models. So I think that especially as models get better, that will be the case kind of moving forward. But yeah, I am looking forward to getting an AI PC, and putting it through its paces eventually.

**Chris Benson:** Yeah. Right now my M2 is through my employer, so my next one will be -- I'm hoping to be ether an M4, and I'm thinking about possibly a non-Apple one as well. The M4s are supposed to be able to do a quite a bit more than the earlier generations... So looking forward to being able to pursue this.

**Daniel Whitenack:** Yeah, definitely. Well, I hope our audience -- we'll include a few links to some blog posts about these quantization methods, and some of the systems like Ollama and LLM Studio and others that we talked about it. I'd encourage everyone to get hands-on and try your own hand at it, and you'll get a sense for the performance of these models locally. So definitely give it a try.

**Chris Benson:** Alright. Well, thanks a lot, Daniel. That was great information today. It was a good show, and thanks for bringing that.

**Daniel Whitenack:** Yup. We'll talk to you soon.