---
layout: post
title: How to Port-Forward Jupyter Notebooks
subtitle: ...to enable efficient remote-working.
---

[Jupyter notebooks](http://jupyter.org/) and  their related [iTorch notebooks](https://github.com/facebook/iTorch) seem to be popular for tutorials, e.g the [Deep Learning with Torch](https://github.com/soumith/cvpr2015/blob/master/Deep%20Learning%20with%20Torch.ipynb) tutorial I started today, but I hated them and avoided them -- not just for [the reasons on this list](http://opiateforthemass.es/articles/why-i-dont-like-jupyter-fka-ipython-notebook/), but mainly because I keep my "machine learning machine" inside my university's firewall and this has made it a pain to run "notebooks" if you're off-site.


When I work from home, I do so via a couple ssh hops, and then copy and paste my script files into the terminal window.  But these "notebook" things require a web GUI, and X11 forwarding over mutliple ssh sessions is prohibitively slow.


I didn't want to configure a NAT system, and was considering some kind of homegrown CGI-script system (which has "security breach" written all over it), but thankfully I stumbled upon [this post on Coderwall](https://coderwall.com/p/ohk6cg/remote-access-to-ipython-notebooks-via-ssh), where the process was spelled out.  For my set of systems, I needed an additional layer of port-forwarding.  So for me it goes like this...


1. My machine-learning computer, which we'll call "`internal`", sits inside the firewall.  
On internal, I run the Jupyter notebook...  
        `me@internal$ jupyter notebook --no-browser --port=8889`  
or for torch, similarly,  
        `me@internal:~$ itorch notebook --no-browser --port=8889`  
This generates a bunch of text, including a URL with a token. It'll say...

    > Copy/paste this URL into your browser when you connect for the first time, to login with a token:  
    > http://localhost:8889/?token=96c92fc27f102995044da89ae111914c28e51757d57bebfc  

2. The server we'll call "`doorkeeper`" is visible to the outside world, and so we forward its port 8889 to the one over on "`internal`" where the notebook is running:  
        `me@doorkeeper:~$ ssh -N -n -L 127.0.0.1:8889:127.0.0.1:8889 internal`


3. Then on my laptop, I run a similar port-forward so the browser will connected to the port on `doorkeeper`:  
        `me@laptop:~$ ssh -N -n -L 127.0.0.1:8889:127.0.0.1:8889 doorkeeper`  


4. And then on my laptop, I paste the URL from the jupyter (or itorch) notebook into my web browser...  
    `http://localhost:8889/?token=96c92fc27f102995044da89ae111914c28e51757d57bebfc`  
**...and it works!**  The notebook comes right up, but the only lag involves sending *text* over ssh, as opposed to sending X11 graphics.


(incidentally, I find 'localhost' sometimes doesn't resolve, which is why I use 127.0.0.1 explicitly)




**Wohoo!**

<hr>
## Extra: Remotely Editing Files via rmate & Sublime Text

On laptop, in Sublime Text 3: Tools > Command Pallete > Install package > rsub

On internal (server): `sudo apt-get install ruby; sudo gem install rmate`

Make two reverse-SHH tunnel hops from laptop to doorkeeper to internal:

1.  `ssh -R 52698:127.0.0.1:52698 doorkeeper`

2.  (on doorkeeper) `ssh -R 52698:127.0.0.1:52698 internal`

3.  (then on internal) `rmate [whatever file you want to edit]`

**...and suddenly, your file appears in your Sublime Text window on your laptop!**

To automate this, either alias ssh to be "ssh -R 52698:127.0.0.1:52698" or modify your ~/.ssh/config file(s)
