**审稿人1：8-strong**

Could the authors elaborate on how the dimension-specific convolutions adapt to different signal characteristics? A more detailed explanation of this adaptation process would strengthen the paper's contribution

介绍核心创新点和CNet的不同



The paper could benefit from more detailed guidelines on hyperparameter selection, particularly for the cut-off ratio ωc. Additionally, while the theoretical analysis is thorough, some concepts could be explained more intuitively. 

cut-off ratio的实验 然后 介绍下订立不用

**审稿人2：7-Clear**

\* While the authors establish convergence guarantees, the complexity analysis focuses on per-iteration cost but not discuss the overall convergence speed across epochs.

+讨论和收敛实验

\* The paper lacks discussion on inference speed and hardware efficiency, particularly when applied to real-time signal processing.

+讨论和硬件实验

\* Why only plots for seismic data? Need to include empirical convergence plots for all datasets.

+结论一致的 加图片

\* Need to provide runtime comparisons and discuss the feasibility of deploying ConFact on edge devices or real-time systems.

提供讨论

**审稿人3：5-Boardline**

1. The organization of the work should be further improved. Especially for the method section, each module should be separately introduced.

   我们已经把各个章节分开了

2. The denoising effect of the work is not well illustrated. For the figures in supplementary materials, some reconstructed images do not clearly demonstrate the superiority of the work to other works. Maybe more examples can be provided, including original images, the nosiy ones, and reconstructed ones.

   一个为了的模块既能对噪声有提升 也能对reconstruction有提升 就增强了鲁棒性。我们把一些信号的先验放进了张量分解中让他更适合信号处理。

3. For the motivations, the authors claimed that existing tensor factorization methods do not provide satisfactory denoising performance, could the author provide more theoretical justifications?

   这个有引用。

   我们的解决办法是采用中间结果的cutoff来去除不合理的部分，简单有效并且适用于denoising和reconstruction都会有用。

4. There are some other works that also consider tensor factorization and convolution simultaneously. What distinguishes this work from existing methods?

   其他paper的结合是主要集中在convolution网络的压缩和高效inference，而非对于信号本身的处理。我们是在于信号侧的处理而非网络端。这个是有着巨大的不同。



**审稿人4：**

和Cnet绝对不同。

Cnet是bibatch的拓展，从二维到三维，考虑了信号的高维度特性，是很大的不同，

我们的核心motivation：

1. 考虑某些维度不变特性，把conv按照dimention-wise的方式加进来。这使得我们能够对于很多有dimention-wise信号也能很好处理，就比如地震和音频数据，这些是CNet欠缺的地方。
2. 考虑到信号本身的ratio特性，把ratio控制模块加进来，使得能够更好理解信号。在重构和去噪都能很好，我们本身不是为了去噪专门设计的，只是由于我们发现效果好加上去了。我们展示了更进一步的鲁棒性这是CNet不具备的。
3. 我们的优化算法loss设计也不一样。denoising supervision保证了鲁棒性。我们的设计其实对于denoising和重构一样，因为我们任务重构缺失本质上也有noise，这是我们的直觉。

