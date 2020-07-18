This has been my personal reading list, first compiled ca. February 2016 & updated very infrequently (e.g. Oct 2016, Feb 2017, Sept 2017).  The field moves so quickly, much of this may have been superseded by now.  If you find it useful as well, that's great.

*I'm mostly interested in audio processing, so...* 

### Jump Right Into : Audio Processing via RNNs:

* Generation/Synthesis of new sounds based on training set:

    * Jake Fiala: "Deep Learning and Sound" <http://fiala.uk/notes/deep-learning-and-sound-01-intro>
    * GRUV: <https://github.com/MattVitelli/GRUV>.  Btw, found that LSTM worked better than GRU.
    * John Glover: <http://www.johnglover.net/blog/generating-sound-with-rnns.html>  Glover used LSTM fed by phase vocoder (really just STFT).
    * Google Magenta for MIDI: <https://magenta.tensorflow.org/welcome-to-magenta>
    * Google WaveNet for Audio... <https://deepmind.com/blog/wavenet-generative-model-raw-audio/>
        * WaveNet is slow.   "Fast Wavenet": <https://github.com/tomlepaine/fast-wavenet>
        * WaveNet in Keras: <https://github.com/basveeling/wavenet>

### General Neural Network References:

* Books/Guides on Deep/Machine Learning: (all excellent)
    * <http://neuralnetworksanddeeplearning.com>
    * <http://machinelearningmastery.com>
    * <https://www.deeplearningbook.org>
    * [Hacker's Guide to Neural Nets](http://karpathy.github.io/neuralnets/) by karpathy
* Tutorials/Videos:
    * Youtube Playlist on “Deep Learning”, t from Oxford U. by Nando de Freitas <https://www.youtube.com/playlist?list=PLE6Wd9FR--EfW8dtjAuPoTuPcqmOV53Fu>
    * Andrew Ng's online course on ML at Stanford comes highly recommended: <http://www.youtube.com/view_play_list?p=A89DCFA6ADACE599>
    * Stanford Tutorial: <http://ufldl.stanford.edu/tutorial/>
*  Concepts in NN/Deep Learning:
    * Backpropagation (i.e. the chain rule): 
        * - [neuralnetworksanddeeplearning.org book, chapter 2](http://neuralnetworksanddeeplearning.com/chap2.html)
        * -  Chris Olah on backprop: <http://colah.github.io/posts/2015-08-Backprop/>
        * - Karpathy on backprop: <http://cs231n.github.io/optimization-2/>


### Recurrent Neural Networks (RNN) (which mostly feature LSTM nowadays):

* RNNs in general:
    * Karpathy post: <http://karpathy.github.io/2015/05/21/rnn-effectiveness/, Karpathy talk: https://www.youtube.com/watch?v=yCC09vCHzF8>
        * Excellent annotated Char-NN in Keras tutorial: <http://ml4a.github.io/guides/recurrent_neural_networks/>
    * Andrew Trask post/tutorial: <https://iamtrask.github.io/2015/11/15/anyone-can-code-lstm/>
    * Denny Britz post: <http://www.wildml.com/2015/09/recurrent-neural-networks-tutorial-part-1-introduction-to-rnns/>
    * Class notes/tutorial (long!): <http://minds.jacobs-university.de/sites/default/files/uploads/papers/ESNTutorialRev.pdf>
    * CS class notes (short): <https://www.willamette.edu/~gorr/classes/cs449/rnn1.html>
    * Excellent post by Ross Goodwin RNNs: <https://medium.com/@rossgoodwin/adventures-in-narrated-reality-6516ff395ba3#.q2xh8dp5t>
    * Great List of references; <https://handong1587.github.io/deep_learning/2015/10/09/rnn-and-lstm.html>
* in TensorFlow: <https://www.tensorflow.org/versions/r0.8/tutorials/recurrent/index.html>
* Theano tutorial:  <http://deeplearning.net/tutorial/rnnslu.html>
* Batch Normalization for: <https://arxiv.org/abs/1510.01378>: *"applying batch normalization to the hidden-to-hidden transitions of our RNNs doesn't help the training procedure. We also show that when applied to the input-to-hidden transitions, batch normalization can lead to a faster convergence of the training criterion but doesn't seem to improve the generalization performance"*

*Traditional RNNs suffer from vanishing/exploding gradient. Hence LSTM & others...*

### Long Short-Term Memory (LSTM):

* Tutorial: <http://nbviewer.jupyter.org/github/JonathanRaiman/theano_lstm/blob/master/Tutorial.ipynb>
* Chris Olah post: <http://colah.github.io/posts/2015-08-Understanding-LSTMs>
* Zach Lipton post, "Demystifying LSTM" (with Tutorial theano code): <http://blog.terminal.com/demistifying-long-short-term-memory-lstm-recurrent-neural-networks/>
* Demo: Lightweight Theano-LSTM: <https://github.com/JonathanRaiman/theano_lstm>
* Massive 33-page review article by Lipton et al: <http://arxiv.org/abs/1506.00019>
* As of March 2016, Keras forum posts show that "stated" RNNs are still an active dev issue. (As of last year, Keras has LSTM but was resetting the "state", = inconvenient & slow.)....Update Sept 2016: Seems to be fixed
* LSTM tutorial in Tensorflow: <https://www.tensorflow.org/versions/r0.10/tutorials/recurrent/index.html>
* Stateful LSTM in Keras for time-series prediction: <https://github.com/fchollet/keras/blob/master/examples/stateful_lstm.py>
    * Much-need Docs on stateful LSTM in Keras: <http://philipperemy.github.io/keras-stateful-lstm/>
* Tensorflow sequence prediction: <http://mourafiq.com/2016/05/15/predicting-sequences-using-rnn-in-tensorflow.html>
* LSTM backpropagation tutorial :-)   <http://arunmallya.github.io/writeups/nn/lstm/index.html#/>


### LSTM Alternatives/advances:

* GRU (Gated Recurrent Unit) by Cho et al, "Learning Phrase Representations using RNN Encoder–Decoder for Statistical Machine Translation", <http://arxiv.org/pdf/1406.1078v3.pdf>  (2014)
    * Chung et al. Good exp of GRU & LSTM, say GRU comparable to LSTM,  <http://arxiv.org/abs/1412.3555>
    * But GRUV/MVitelli found that LSTM outperformed GRU for audio accuracy
    * GRU's are a bit simpler than LSTM, Britz blog/tutorial: <http://www.wildml.com/2015/10/recurrent-neural-network-tutorial-part-4-implementing-a-grulstm-rnn-with-python-and-theano>
* ClockWork-RNN by Koutnik et al,  <http://arxiv.org/pdf/1402.3511v1.pdf>
* Highway networks...
* Echo State Networks (ESN).  (2008) Comparison of MLP, RNN & ESN for sequence modeling: <https://www.researchgate.net/publication/224374378_A_comparison_of_MLP_RNN_and_ESN_in_determining_harmonic_contributions_from_nonlinear_loads>
* Undecimated Fully Convolutional Neural Networks (UFCNN): <http://arxiv.org/pdf/1508.00317.pdf>
* ConvNet for Audio -- Spotify analysis & recommendation: <http://benanne.github.io/2014/08/05/spotify-cnns.html>

### LSTM for Sequence to Sequence Learning:

- Main paper: <http://papers.nips.cc/paper/5346-sequence-to-sequence-learning-with-neural-networks.pdf>
- There’s an encoder step and a decoder step
- Example: <https://bigaidream.gitbooks.io/subsets_ml_cookbook/content/dl/theano/theano_keras_sequence2sequence.html#keras-for-sequence-to-sequence-learning>
- Keras Seq2Seq extension: <https://github.com/farizrahman4u/seq2seq>
- Multiple blog pages, re. language model: <https://indico.io/blog/sequence-modeling-neuralnets-part1/>
- Tensor flow tutorial: <https://www.tensorflow.org/versions/r0.10/tutorials/seq2seq/index.html>  WARNING: “It takes about 18GB of disk space and several hours to prepare the training corpus.” :-(
- SE post on pitch-shift mapping <http://stats.stackexchange.com/questions/220307/rnn-learning-sine-waves-of-different-frequencies>
- Denoising:
    - <http://mlsp.cs.cmu.edu/people/rsingh/docs/waspaa2015.pdf>
    - Denoising Autoencoder: <https://www.quora.com/Is-it-possible-to-create-an-adaptive-filter-using-neural-network-so-that-after-training-it-can-filter-noisy-signal-and-give-desired-output>,    <https://www.quora.com/Can-a-denoising-autoencoder-remove-or-filter-noise-in-a-noisy-signal-like-audio-and-recover-the-clean-signal>
    - Dereverberation:

### Extended Memory Architectures:
* Memory Networks, Weston,
    * First paper: <https://arxiv.org/abs/1410.3916.  >
    * Tutorial: <http://www.thespermwhale.com/jaseweston/icml2016/>
    * End-to-End version: <http://arxiv.org/abs/1503.08895>
    * Keras version: <https://github.com/fchollet/keras/blob/master/examples/babi_memnn.py>
* Stack-Augmented Recurrent Nets, Joulin & Mikolov  "Inferring Algorithmic Patterns with Stack-Augmented Recurrent Nets," <https://arxiv.org/pdf/1503.01007.pdf (2015)>
* Neural Turing Machines (NTM), Graves et al, <https://arxiv.org/pdf/1410.5401v2.pdf>
* Neural Stack Machines:
	- Original paper: "Learning to Transduce with Unbounded Memory" by Grefenstette et al.: <https://arxiv.org/abs/1506.02516>
	- [Trask's tutorial blog on Neural Stack Machines](http://iamtrask.github.io/2016/02/25/deepminds-neural-stack-machine/)

### Convolutional Neural Networks:
* Video: "What is wrong with convolutional neural nets?" Geoffrey Hinton,  Fields Institute, August 2017"<https://www.youtube.com/watch?v=Mqt8fs6ZbHk&feature=youtu.be>
* Excellent: "History of major convnet architectures" (LeNet, AlexNet, Inception ResNet, VGG,...) <https://culurciello.github.io/tech/2016/06/04/nets.html>
* Excellent: "A guide to convolution arithmetic for deep learning" by Dumoulin and Visin <https://arxiv.org/pdf/1603.07285.pdf>
* Glossary/Summary of conv net terms/concepts:
	- **Vector:** *not* a true vector in the sense of vector calculus. Just a one-dimensional array. "N-dimensional vector" = 1-D array with N elements.
	- **Tensor:** *not* a true tensor in the sense of differential geometry. Just a multi-dimensional arry or "matrix".
	- **Affine Transformation:** General math term; here we just mean multiplying by a tensor and (maybe) adding a constant bias (vector).  Generalization of "linear transformation."
	- **Convolution:** Pretty much what you'd normally think of "convolution" in the DSP sense.  *The following analogy helps me too: Evaluating a finite-difference stencil on a discretised scalar field via a banded (e.g. tridiagonal) matrix would be considered a convolution in the CNN sense, because said matrix is sparse and the same weights are used throughout.*
	- **Channel Axis:** (quoting D&V): "is used to access different views of the data (e.g., the red, green and blue channels of a color image, or the left and right channels of a stereo audio track)."
	- **Feature Map:** Generally, the output of running one particular convolution kernel over a data item (e.g over an image). However there are also *input feature maps*, examples of which are the "channels" referred to earlier (e.g. RGB, Left/Right). 
	- **Flattening:** turn a tensor into a vector
	- **Pooling:** can think of it like a special type of convolution kernel (except it may not just add up the kernel's inputs). Usually "Max Pooling", as in: take the maximum value from the the kernel's inputs.  (On the other hand, "Average pooling" really is just a regular top-hat convolution.) In contrast to regular convolution, pooling does not involve zero padding, and pooling often takes place over non-overlapping regions of the input.
	- **(Zero-)Padding:** Pretty much like in the DSP sense: add zeros to the front or end of a data stream or image, so that you can run convolution kernel all the way up to & over the boundaries of where they data's defined.
	- **Transposed Convolution:** Analagous to transposing a matrix to get an output with oppositely-ordered shape, e.g. to go from an output feature map of one shape, back to the original shape of the input.   *There seems to be some confusion, whereby some people treat the transpose as if it's an inverse, like $$A^T A = I$$. ??*
	- **1x1:** Actually 1x1xC, where C is, e.g. the number color channels in a RGB image (3).

	- *an observation: the bigger shape of the kernel, the smaller the shape of its output feature map*
* Related: Deconvolutional Networks <http://www.matthewzeiler.com/pubs/cvpr2010/cvpr2010.pdf>


### Reinforcement Learning:

* OpenAIGym: <https://openai.com/blog/openai-gym-beta/>
    * Tutorial for cart-pole problem: <http://kvfrans.com/simple-algoritms-for-solving-cartpole/>
* For games: Giraffe
* Atari DRL: Video: <https://www.youtube.com/watch?v=V1eYniJ0Rnk>
* BetaGo: <https://github.com/maxpumperla/betago>


### Data Representation:

Scattering Hierarchy (multi-scale representation) by Mallat (2012-2014), Pablo Sprechman's talk <https://youtu.be/OS6rZXKVU1Y?t=20m44s>



### Related Approaches to Neural Networks:  (historical)

* Hidden Markov Models (HMM).  Dahl used for text classification: George E. Dahl, Ryan P. Adams, and Hugo Larochelle. "Training restricted boltzmann machines on word observations." arXiv:1202.5695v1 (2012)
* Support Vector Machine (SVM).  SVMs are globally convex, which is nice (whereas NNs are only locally convex).  Very effective for classification tasks.  But NNs have beat them out for complex datasets & tasks.   Audio app:  e.g., Audio Classificiation by Gou & Li (2003) <http://www.ee.columbia.edu/~sfchang/course/spr-F05/papers/guo-li-svm-audio00.pdf>
* Restricted Boltzmann Machine (RBM).  Hinton et al. mid-2000s



### Frameworks (too many to choose from!):

* Main Ones:
    * [Theano](http://deeplearning.net/software/theano/) - mature codebase, non-CUDA GPU support via libgpuarray
    * [TensorFlow](https://www.tensorflow.org/) - Google-supported, awesome viz tool TensorBoard
    * [Keras](http://keras.io), runs on Theano or TensorFlow as backends. VERY popular
    * [Torch](http://torch.ch/) - used by LeCun & Karpathy, scripting in Lua.  Not Python.  
    	  * [PyTorch](http://pytorch.org/) Python bindings for Torch, includes 'automatic differentiation'

    * [Scikit-Learn](http://scikit-learn.org) - General system for many methods; some Keras support.  Allows 'easy' swapping of different ML methods & models

* Others, not seeing these used as much:
    * [Caffe](http://caffe.berkeleyvision.org/), supposed to be easy & abstract
    * [Lasagne](http://lasagne.readthedocs.io/en/latest/) - Another Theano front end for abstraction & ease of use
    * [Mozi](https://github.com/hycis/Mozi), Another one build on Theano.  Looks simple to use
    * [DeepLearning4J](https://deeplearning4j.org/): The "J" is for "Java"
    * scikits.neural - not popular
* Which package to choose when starting out?
    * I say **Keras**.  Everything's super-easy and automated compared to others.




### More Tutorials (e.g., app-specific):

* Lots in <http://maachinelearningmastery.com>
* [Andrew Trask’s Blog](http://iamtrask.github.io): Andrew writes excellent tutorials.  The first LSTM guide I read was his. 
* Tutorials on Theano, Keras, Lasagne, RNN: <https://github.com/Vict0rSch/deep_learning>
* Theano:
    * Theano basics:  <http://nbviewer.jupyter.org/github/craffel/theano-tutorial/blob/master/Theano%20Tutorial.ipynb>
    * Then crash course via code: <https://github.com/Newmu/Theano-Tutorials>
    * LSTM in Theano:  <http://nbviewer.jupyter.org/github/JonathanRaiman/theano_lstm/blob/master/Tutorial.ipynb>
* Tensorflow:
    * TensorFlow graph vis tutorial: <https://www.tensorflow.org/versions/r0.8/how_tos/graph_viz/index.html>
    * TensorFlow on AWS (tutorial video): <https://www.youtube.com/watch?v=1QhCsO4jmoM>
    * LSTM tutorial in Tensorflow: <https://www.tensorflow.org/versions/r0.10/tutorials/recurrent/index.html>
* Torch:
    * First, Lua: "Learn Lua in 15 Minutes": <http://tylerneylon.com/a/learn-lua/>
    * Deep Learning in Torch: a 60-minute Blitz by Soumith Chintala at CVPR2015: <https://github.com/soumith/cvpr2015/blob/master/Deep%20Learning%20with%20Torch.ipynb>
    * LSTM in Torch (by Zaremba) <https://github.com/wojzaremba/lstm>
    * Tutorial Videos: <https://www.youtube.com/playlist?list=PLLHTzKZzVU9ebuL6DCclzI54MrPNFGqbW>
  

### More Demos:

* Anything by [@karpathy](http://karpathy.github.io/)
* Lightweight Theano-LSTM: <https://github.com/JonathanRaiman/theano_lstm>
* TensorFlow Playgrounds: <http://playground.tensorflow.org >


### Audio Applications:

* Huang et al, "Deep Recurrent NNs for Source Separation" <http://posenhuang.github.io/papers/Joint_Optimization_of_Masks_and_Deep%20Recurrent_Neural_Networks_for_Monaural_Source_Separation_TASLP2015.pdf>
    *  Qutoe: "in parallel, for improving the efficiency of DRNN training, utterances are chopped into sequences of at most 100 time steps"
* Ron Weiss (Google) talk: "Training neural network acoustic models on waveforms" <https://www.youtube.com/watch?v=sI_8EA0_ha8>
* Music comp: <http://www.hexahedria.com/2015/08/03/composing-music-with-recurrent-neural-networks/>
* Predict time sequence with LSTM & Theano...GRUV
* MULTI-RESOLUTION LINEAR PREDICTION BASED FEATURES FOR AUDIO ONSET DETECTION WITH BIDIRECTIONAL LSTM NEURAL NETWORKS Erik Marchi1 , Giacomo Ferroni2 , Florian Eyben1 , Leonardo Gabrielli2 , Stefano Squartini2 , Bjorn Schuller ¨ 3,1  <http://mediatum.ub.tum.de/doc/1238131/865625.pdf>
* John Glover on generating instrument sounds with RNN: <http://www.johnglover.net/blog/generating-sound-with-rnns.html>
* Example of using spectrograms as images (for an image-based classifier): <http://stackoverflow.com/questions/37213388/keras-accuracy-does-not-change>



### Datasets of (mostly musical) Audio for Machine Learning:

- IRMAS: for musical Instrument recognition: <http://www.mtg.upf.edu/download/datasets/irmas>

- Fraunhofer IDMT datasets: (Scroll down to “Published Datasets” on <http://www.idmt.fraunhofer.de/en/business_units/m2d/research.html)>
    * 		IDMT-SMT-Bass  An audio database for bass transcription and signal processing
    * 		IDMT-SMT-Audio-Effects An audio database for automatic effect detection in recordings of electric guitar and bass
    * 		IDMT-SMT-Bass Synthesis A Digital Waveguide Model of the Electric Bass Guitar including Different Playing Techniques
    * 		IDMT-SMT-BASS-SINGLE-TRACK
    * 		Multi-track studio recordings of live performances in Swing, Blues and Funk styles
    * 		IDMT-SMT-Guitar An audio database for guitar transcription and signal processing
    * 		IDMT-SMT-Drums An audio database for drum transcription and source separation
    * 		Multicodec Invdec Tampering Dataset

- Massive list of datasets (most are MIDI though): <http://www.audiocontentanalysis.org/data-sets/>
- Another massive list of datasets (with many repeats from above): <http://wiki.schindler.eu.com/doku.php?id=datasets:overview>

- Melody annotation dataset: <http://medleydb.weebly.com/description.html>

- Binaural audio: :
    * Antoine Deleforge: <http://perception.inrialpes.fr/~Deleforge/AVASM_Dataset/>

### Activations & Optimizers
* ELU: Exponential Linear Unit, seems to work better than ReLU in many cases <https://arxiv.org/pdf/1511.07289v1.pdf>

## In Physics:
* "Fast cosmological parameter estimation using neural networks", T. Auld, M. Bridges, M.P. Hobson and S.F. Gull,  MNRAS. 000, 1–6 (2004), <https://arxiv.org/pdf/astro-ph/0608174.pdf>
* "Parameterized Neural Networks for High-Energy Physics", Baldi, P., Cranmer, K., Faucett, T., Sadowski, P., Whiteson, D. The European Physical Journal C. 76, 235, 1-7, May 2016, 2016, <https://arxiv.org/pdf/1601.07913.pdf>

### Hardware:

* Amazon Web Services (AWS):
    * Stanford disk image (AMI) with everything preinstalled: <https://cs231n.github.io/aws-tutorial/>
    * ...or just grab some other "Community AMI" with CUDA etc installed
    * Another AWS setup: <https://github.com/andreasjansson/simple-aws-gpu-setup>
    * TensorFlow on AWS (tutorial video): <https://www.youtube.com/watch?v=1QhCsO4jmoM>
    * My AWS Aetup:  ```ami-a96285c4```
   ( AMI: old cuda but works: ami-63bf8209   do not like: 11777_MML (ami-37a58f5d) or DeepestLearning )
When u create your own AMI it brings your server down. :-(

```
pip install --upgrade pip
pip install -U numpy
sudo pip install git+git://github.com/Theano/Theano.git --upgrade --no-deps
sudo pip install awscli h5py
git clone <https://github.com/fchollet/keras.git>
cd keras
sudo python setup.py install
```

FACTOR OF 10 SPEEDUP using the g2.xlarge GPUs vs my Macbook Pro (no GPU)!!


### Checkpointing:

run 'watch' command to execute AWS transfer to S3 ever <n> seconds
...and spot instance went down without any checkpoint
to allow uploading from EC2 to S3 it's convoluted:
install aws cli
create an "IAM" user.  Grant the user permissions to upload to s3 via <https://forums.aws.amazon.com/thread.jspa?messageID=600007>
aws configure
...good to go.

```watch -n 550 aws s3 cp /tmp/weights.hdf5 s3://hawleymainbucket```

* Theano GPU setup guide: <https://github.com/andreasjansson/simple-aws-gpu-setup>
* OpenMP: Don't forget to enable multiple OpenMP threads!  Can get you at least a factor of 2 speedup!
    * In most ‘modern’ Python installations (e.g. anaconda) OpenMP is automatic
* My proposed PC build: <https://pcpartpicker.com/user/drscotthawley/saved/bFZ8dC>
* 




### Self-Organizing Maps:

* “Unsupervised Classification of Audio Signals by Self-Organizing Maps and Bayesian Labeling”: <http://link.springer.com/chapter/10.1007%2F978-3-642-28942-2_6>
* “Visualization of Tonal Content in the  Symbolic and Audio Domains“ <http://www.ccarh.org/publications/cm/15/cm15-10-toiviainen.pdf>


### "Weird Stuff":

* Stochastic path Deep NN for image rec: <http://arxiv.org/pdf/1603.09382v1.pdf>


