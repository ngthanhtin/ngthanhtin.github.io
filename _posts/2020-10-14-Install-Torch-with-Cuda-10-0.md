---
layout: post
title: Install Torch with Cuda 10.0
subtitle: Nvidia
gh-repo: daattali/beautiful-jekyll
gh-badge: [settings]
tags: [cuda, nvidia, ubuntu]
comments: true

---
Hi các bạn, ở bài viết này mình sẽ huong dan cac ban cach cai dat Torch va cach lam sao de Torch lam viec voi cuda 10.0
# in a terminal, run the commands WITHOUT sudo
git clone https://github.com/torch/distro.git ~/torch --recursive
cd ~/torch; bash install-deps;

O buoc nay, cac ban co the go:
./install.sh
de cai dat, nhung no chi lam viec voi cuda 5.0

Vi vay, neu muon lam viec voi cuda 10.0, ban se lam them nhung buoc sau day:
1. Install the latest CMake from github repo (the latest FindCUDA.cmake will be installed)
sudo apt-get purge cmake
git clone https://github.com/Kitware/CMake.git
cd CMake
./bootstrap; make; sudo make install

2. Remove FindCUDA.cmake.
cd ~/torch
rm -fr cmake/3.6/Modules/FindCUDA*

3. Apply the following patch to cutorch
diff --git a/lib/THC/THCAtomics.cuh b/lib/THC/THCAtomics.cuh
index 400875c..ccb7a1c 100644
--- a/lib/THC/THCAtomics.cuh
+++ b/lib/THC/THCAtomics.cuh
@@ -94,6 +94,7 @@ static inline __device__ void atomicAdd(long *address, long val) {
 }
 
 #ifdef CUDA_HALF_TENSOR
+#if !(__CUDA_ARCH__ >= 700 || !defined(__CUDA_ARCH__) )
 static inline  __device__ void atomicAdd(half *address, half val) {
   unsigned int * address_as_ui =
       (unsigned int *) ((char *)address - ((size_t)address & 2));
@@ -117,6 +118,7 @@ static inline  __device__ void atomicAdd(half *address, half val) {
    } while (assumed != old);
 }
 #endif
+#endif

cd extra/cutorch
cat > atomic.patch
<copy and paste the patch>
patch -p1 < atomic.patch

4. Build
 ./clean.sh
export TORCH_NVCC_FLAGS="-D__CUDA_NO_HALF_OPERATORS__"
./install.sh

5. Install Cudnn
git clone https://github.com/soumith/cudnn.torch -b R7
cd cudnn.torch
luarocks make cudnn-scm-1.rockspec

[Source](https://github.com/torch/cutorch/issues/834)
