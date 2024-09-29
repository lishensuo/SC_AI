- 主要参考：https://github.com/bowang-lab/scGPT/issues/153 from **wenghan1** 



```shell
conda create -n scgpt_2
conda activate scgpt_2
conda install python=3.10
conda install -c conda-forge cudatoolkit=11.7 cudatoolkit-dev 'gxx>=6.0.0,<12.0' cudnn
# 这一步需要的时间比较久 > 10min
```



```shell
# 这一步需要下载指定版本的torch系列
# 但国内从 https://download.pytorch.org/whl/cu117 下载比较慢
pip install torch==1.13.0+cu117 torchvision==0.14.0+cu117 torchaudio==0.13.0 --extra-index-url https://download.pytorch.org/whl/cu117

# 这里我们从阿里镜像源下载whl文件，然后pip本地安装
# https://mirrors.aliyun.com/pytorch-wheels/cu117/
pip install 'torch-1.13.0+cu117-cp310-cp310-linux_x86_64.whl' -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install 'torchvision-0.14.0+cu117-cp310-cp310-linux_x86_64.whl' -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install 'torchaudio-0.13.0+cu117-cp310-cp310-linux_x86_64.whl' -i https://pypi.tuna.tsinghua.edu.cn/simple
```



```python
pip install packaging -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install flash-attn==1.0.4 --no-build-isolation
# 这一步需要的时间比较久，需要耐心等待
```



```python
conda install r-base r-devtools
pip install --no-deps scgpt

pip install scgpt -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install torch==1.13.0 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install torchtext==0.14.0 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install pyro-ppl==1.8.6 -i https://pypi.tuna.tsinghua.edu.cn/simple
```



```shell
pip install ipykernel
python -m ipykernel install --user --name=scgpt_2
# 如果是conda可以一步到位
```



```python
pip install pandas==1.5.3
pip install scanpy
pip install scvi-tools==0.20.2

pip install numba --upgrade
pip install numpy==1.24.4
pip install torchtext==0.14.0

pip install scib
pip install datasets==2.14.5 transformers==4.33.2
```



```python
pip install pyro-ppl==1.8.6 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install cell-gears==0.0.1 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install orbax==0.1.0 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install gseapy -i https://pypi.tuna.tsinghua.edu.cn/simple
```





其它:

（1）scipy   https://github.com/bowang-lab/scGPT/issues/254

```python
layer_data = layer_data.A if issparse(layer_data) else layer_data
# To
layer_data = layer_data.toarray() if issparse(layer_data) else layer_data
```

（2）pandas 2.0 

```python
df = df.append(out, ignore_index=True)
# To
df = pd.concat([df, out], ignore_index=True)
```







```yaml
name: scgpt_2
channels:
  - conda-forge
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - defaults
dependencies:
  - _libgcc_mutex=0.1=conda_forge
  - _openmp_mutex=4.5=2_gnu
  - _r-mutex=1.0.1=anacondar_1
  - _sysroot_linux-64_curr_repodata_hack=3=h69a702a_16
  - binutils_impl_linux-64=2.43=h4bf12b8_0
  - bwidget=1.9.14=ha770c72_1
  - bzip2=1.0.8=h4bc722e_7
  - c-ares=1.33.1=heb4867d_0
  - ca-certificates=2024.8.30=hbcca054_0
  - cairo=1.18.0=hebfffa5_3
  - cuda-version=11.7=h67201e3_3
  - cudatoolkit=11.7.1=h4bc3d14_13
  - cudatoolkit-dev=11.7.0=h1de0b5d_6
  - cudnn=9.2.1.18=h93471f6_0
  - curl=8.10.1=hbbe4b11_0
  - expat=2.6.3=h5888daf_0
  - font-ttf-dejavu-sans-mono=2.37=hab24e00_0
  - font-ttf-inconsolata=3.000=h77eed37_0
  - font-ttf-source-code-pro=2.038=h77eed37_0
  - font-ttf-ubuntu=0.83=h77eed37_2
  - fontconfig=2.14.2=h14ed4e7_0
  - fonts-conda-ecosystem=1=0
  - fonts-conda-forge=1=0
  - freetype=2.12.1=h267a509_2
  - fribidi=1.0.10=h36c2ea0_0
  - gcc=11.4.0=h602e360_13
  - gcc_impl_linux-64=11.4.0=h00c12a0_13
  - gfortran_impl_linux-64=7.5.0=h56cb351_20
  - graphite2=1.3.13=h59595ed_1003
  - gsl=2.7=he838d99_0
  - gxx=11.4.0=h602e360_13
  - gxx_impl_linux-64=11.4.0=h634f3ee_13
  - harfbuzz=9.0.0=hda332d3_1
  - icu=75.1=he02047a_0
  - kernel-headers_linux-64=3.10.0=h4a8ded7_16
  - keyutils=1.6.1=h166bdaf_0
  - krb5=1.21.3=h659f571_0
  - ld_impl_linux-64=2.43=h712a8e2_0
  - lerc=4.0.0=h27087fc_0
  - libblas=3.9.0=24_linux64_openblas
  - libcblas=3.9.0=24_linux64_openblas
  - libcurl=8.10.1=hbbe4b11_0
  - libdeflate=1.21=h4bc722e_0
  - libedit=3.1.20191231=he28a2e2_2
  - libev=4.33=hd590300_2
  - libexpat=2.6.3=h5888daf_0
  - libffi=3.4.2=h7f98852_5
  - libgcc=14.1.0=h77fa898_1
  - libgcc-devel_linux-64=11.4.0=h8f596e0_113
  - libgcc-ng=14.1.0=h69a702a_1
  - libgfortran-ng=7.5.0=h14aa051_20
  - libgfortran4=7.5.0=h14aa051_20
  - libgfortran5=14.1.0=hc5f4f2c_1
  - libgit2=1.8.1=he8d1d4c_1
  - libglib=2.80.3=h315aac3_2
  - libgomp=14.1.0=h77fa898_1
  - libiconv=1.17=hd590300_2
  - libjpeg-turbo=3.0.0=hd590300_1
  - liblapack=3.9.0=24_linux64_openblas
  - libnghttp2=1.58.0=h47da74e_1
  - libnsl=2.0.1=hd590300_0
  - libopenblas=0.3.27=pthreads_hac2b453_1
  - libpng=1.6.44=hadc24fc_0
  - libsanitizer=11.4.0=h5763a12_13
  - libsqlite=3.46.1=hadc24fc_0
  - libssh2=1.11.0=h0841786_0
  - libstdcxx=14.1.0=hc0a3c3a_1
  - libstdcxx-devel_linux-64=11.4.0=h8f596e0_113
  - libstdcxx-ng=14.1.0=h4852527_1
  - libtiff=4.7.0=h6565414_0
  - libuuid=2.38.1=h0b41bf4_0
  - libuv=1.48.0=hd590300_0
  - libwebp-base=1.4.0=hd590300_0
  - libxcb=1.16=hb9d3cd8_1
  - libxml2=2.12.7=he7c6b58_4
  - libzlib=1.3.1=h4ab18f5_1
  - make=4.4.1=hb9d3cd8_1
  - ncurses=6.5=he02047a_1
  - openssl=3.3.2=hb9d3cd8_0
  - pandoc=3.4=ha770c72_0
  - pango=1.54.0=h4c5309f_1
  - pcre2=10.44=hba22ea6_2
  - pip=24.2=pyh8b19718_1
  - pixman=0.43.2=h59595ed_0
  - pthread-stubs=0.4=hb9d3cd8_1002
  - python=3.10.11=he550d4f_0_cpython
  - r-askpass=1.2.0=r44hb1dbf0f_1
  - r-assertthat=0.2.1=r44hc72bb7e_5
  - r-base=4.4.1=h518d376_15
  - r-base64enc=0.1_3=r44hb1dbf0f_1007
  - r-brew=1.0_10=r44hc72bb7e_1
  - r-brio=1.1.5=r44hb1dbf0f_1
  - r-bslib=0.8.0=r44hc72bb7e_0
  - r-cachem=1.1.0=r44hb1dbf0f_1
  - r-callr=3.7.6=r44hc72bb7e_1
  - r-cli=3.6.3=r44h0d4f4ea_1
  - r-clipr=0.8.0=r44hc72bb7e_3
  - r-commonmark=1.9.1=r44hb1dbf0f_1
  - r-cpp11=0.5.0=r44hc72bb7e_0
  - r-crayon=1.5.3=r44hc72bb7e_1
  - r-credentials=2.0.1=r44hc72bb7e_1
  - r-curl=5.2.1=r44h6b349a7_1
  - r-desc=1.4.3=r44hc72bb7e_1
  - r-devtools=2.4.5=r44hc72bb7e_3
  - r-diffobj=0.3.5=r44hb1dbf0f_3
  - r-digest=0.6.37=r44h0d4f4ea_0
  - r-downlit=0.4.4=r44hc72bb7e_1
  - r-ellipsis=0.3.2=r44hb1dbf0f_3
  - r-evaluate=1.0.0=r44hc72bb7e_0
  - r-fansi=1.0.6=r44hb1dbf0f_1
  - r-fastmap=1.2.0=r44ha18555a_1
  - r-fontawesome=0.5.2=r44hc72bb7e_1
  - r-fs=1.6.4=r44ha18555a_1
  - r-gert=2.1.2=r44h017ce79_0
  - r-gh=1.4.1=r44hc72bb7e_1
  - r-gitcreds=0.1.2=r44hc72bb7e_3
  - r-glue=1.7.0=r44hb1dbf0f_1
  - r-highr=0.11=r44hc72bb7e_1
  - r-htmltools=0.5.8.1=r44ha18555a_1
  - r-htmlwidgets=1.6.4=r44h785f33e_3
  - r-httpuv=1.6.15=r44ha18555a_1
  - r-httr2=1.0.4=r44hc72bb7e_0
  - r-ini=0.3.1=r44hc72bb7e_1006
  - r-jquerylib=0.1.4=r44hc72bb7e_3
  - r-jsonlite=1.8.9=r44h2b5f3a1_0
  - r-knitr=1.48=r44hc72bb7e_0
  - r-later=1.3.2=r44ha18555a_1
  - r-lifecycle=1.0.4=r44hc72bb7e_1
  - r-magrittr=2.0.3=r44hb1dbf0f_3
  - r-memoise=2.0.1=r44hc72bb7e_3
  - r-mime=0.12=r44hb1dbf0f_3
  - r-miniui=0.1.1.1=r44hc72bb7e_1005
  - r-openssl=2.2.2=r44he8289e2_0
  - r-pillar=1.9.0=r44hc72bb7e_2
  - r-pkgbuild=1.4.4=r44hc72bb7e_1
  - r-pkgconfig=2.0.3=r44hc72bb7e_4
  - r-pkgdown=2.1.1=r44hc72bb7e_0
  - r-pkgload=1.4.0=r44hc72bb7e_0
  - r-praise=1.0.0=r44hc72bb7e_1008
  - r-prettyunits=1.2.0=r44hc72bb7e_1
  - r-processx=3.8.4=r44hb1dbf0f_1
  - r-profvis=0.4.0=r44h2b5f3a1_0
  - r-promises=1.3.0=r44ha18555a_1
  - r-ps=1.7.7=r44hdb488b9_0
  - r-purrr=1.0.2=r44hdb488b9_1
  - r-r6=2.5.1=r44hc72bb7e_3
  - r-ragg=1.3.3=r44h9aa3752_0
  - r-rappdirs=0.3.3=r44hb1dbf0f_3
  - r-rcmdcheck=1.4.0=r44h785f33e_3
  - r-rcpp=1.0.13=r44h0d4f4ea_0
  - r-rematch2=2.1.2=r44hc72bb7e_4
  - r-remotes=2.5.0=r44hc72bb7e_1
  - r-rlang=1.1.4=r44ha18555a_1
  - r-rmarkdown=2.28=r44hc72bb7e_0
  - r-roxygen2=7.3.2=r44h0d4f4ea_1
  - r-rprojroot=2.0.4=r44hc72bb7e_1
  - r-rstudioapi=0.16.0=r44hc72bb7e_1
  - r-rversions=2.1.2=r44hc72bb7e_3
  - r-sass=0.4.9=r44ha18555a_1
  - r-sessioninfo=1.2.2=r44hc72bb7e_3
  - r-shiny=1.9.1=r44h785f33e_0
  - r-sourcetools=0.1.7_1=r44ha18555a_2
  - r-stringi=1.8.4=r44h33cde33_3
  - r-stringr=1.5.1=r44h785f33e_1
  - r-sys=3.4.2=r44hb1dbf0f_2
  - r-systemfonts=1.1.0=r44h38d38ca_1
  - r-testthat=3.2.1.1=r44h0d4f4ea_1
  - r-textshaping=0.4.0=r44ha47bcaa_2
  - r-tibble=3.2.1=r44hdb488b9_3
  - r-tinytex=0.53=r44hc72bb7e_0
  - r-urlchecker=1.0.1=r44hc72bb7e_3
  - r-usethis=3.0.0=r44hc72bb7e_0
  - r-utf8=1.2.4=r44hb1dbf0f_1
  - r-vctrs=0.6.5=r44h0d4f4ea_1
  - r-waldo=0.5.3=r44hc72bb7e_0
  - r-whisker=0.4.1=r44hc72bb7e_2
  - r-withr=3.0.1=r44hc72bb7e_0
  - r-xfun=0.47=r44h0d4f4ea_0
  - r-xml2=1.3.6=r44h8194278_2
  - r-xopen=1.0.1=r44hc72bb7e_1
  - r-xtable=1.8_4=r44hc72bb7e_6
  - r-yaml=2.3.10=r44hdb488b9_0
  - r-zip=2.3.1=r44hb1dbf0f_1
  - readline=8.2=h8228510_1
  - sed=4.8=he412f7d_0
  - setuptools=74.1.2=pyhd8ed1ab_0
  - sysroot_linux-64=2.17=h4a8ded7_16
  - tk=8.6.13=noxft_h4845f30_101
  - tktable=2.10=h8bc8fbc_6
  - wheel=0.44.0=pyhd8ed1ab_0
  - xorg-kbproto=1.0.7=hb9d3cd8_1003
  - xorg-libice=1.1.1=hd590300_0
  - xorg-libsm=1.2.4=h7391055_0
  - xorg-libx11=1.8.9=hb711507_1
  - xorg-libxau=1.0.11=hb9d3cd8_1
  - xorg-libxdmcp=1.1.3=hb9d3cd8_1
  - xorg-libxext=1.3.4=h0b41bf4_2
  - xorg-libxrender=0.9.11=hd590300_0
  - xorg-libxt=1.3.0=hd590300_1
  - xorg-renderproto=0.11.1=hb9d3cd8_1003
  - xorg-xextproto=7.3.0=hb9d3cd8_1004
  - xorg-xproto=7.0.31=hb9d3cd8_1008
  - xz=5.2.6=h166bdaf_0
  - zlib=1.3.1=h4ab18f5_1
  - zstd=1.5.6=ha6fb4c9_0
  - pip:
      - absl-py==2.1.0
      - aiohappyeyeballs==2.4.0
      - aiohttp==3.10.5
      - aiosignal==1.3.1
      - anndata==0.10.8
      - array-api-compat==1.8
      - asttokens==2.4.1
      - async-timeout==4.0.3
      - attrs==24.2.0
      - cached-property==1.5.2
      - cell-gears==0.0.1
      - certifi==2024.8.30
      - charset-normalizer==3.3.2
      - chex==0.1.86
      - comm==0.2.2
      - contextlib2==21.6.0
      - contourpy==1.3.0
      - cycler==0.12.1
      - datasets==2.14.5
      - debugpy==1.8.5
      - decorator==5.1.1
      - deprecated==1.2.14
      - dill==0.3.7
      - docrep==0.3.2
      - einops==0.8.0
      - et-xmlfile==1.1.0
      - etils==1.9.4
      - exceptiongroup==1.2.2
      - executing==2.1.0
      - filelock==3.16.1
      - flash-attn==1.0.4
      - flax==0.9.0
      - fonttools==4.54.0
      - frozenlist==1.4.1
      - fsspec==2023.6.0
      - gseapy==1.1.3
      - h5py==3.11.0
      - huggingface-hub==0.25.1
      - humanize==4.10.0
      - idna==3.10
      - igraph==0.11.6
      - importlib-resources==6.4.5
      - iniconfig==2.0.0
      - ipykernel==6.29.5
      - ipython==8.27.0
      - jax==0.4.33
      - jaxlib==0.4.33
      - jedi==0.19.1
      - jinja2==3.1.4
      - joblib==1.4.2
      - jupyter-client==8.6.3
      - jupyter-core==5.7.2
      - kiwisolver==1.4.7
      - legacy-api-wrap==1.4
      - leidenalg==0.10.2
      - lightning==2.1.4
      - lightning-utilities==0.11.7
      - llvmlite==0.43.0
      - markdown-it-py==3.0.0
      - markupsafe==2.1.5
      - matplotlib==3.9.2
      - matplotlib-inline==0.1.7
      - mdurl==0.1.2
      - ml-collections==0.1.1
      - ml-dtypes==0.5.0
      - mpmath==1.3.0
      - msgpack==1.1.0
      - mudata==0.3.1
      - multidict==6.1.0
      - multipledispatch==1.0.0
      - multiprocess==0.70.15
      - natsort==8.4.0
      - nest-asyncio==1.6.0
      - networkx==3.3
      - numba==0.60.0
      - numpy==1.24.4
      - numpyro==0.15.3
      - nvidia-cublas-cu11==11.10.3.66
      - nvidia-cublas-cu12==12.1.3.1
      - nvidia-cuda-cupti-cu12==12.1.105
      - nvidia-cuda-nvrtc-cu11==11.7.99
      - nvidia-cuda-nvrtc-cu12==12.1.105
      - nvidia-cuda-runtime-cu11==11.7.99
      - nvidia-cuda-runtime-cu12==12.1.105
      - nvidia-cudnn-cu11==8.5.0.96
      - nvidia-cudnn-cu12==9.1.0.70
      - nvidia-cufft-cu12==11.0.2.54
      - nvidia-curand-cu12==10.3.2.106
      - nvidia-cusolver-cu12==11.4.5.107
      - nvidia-cusparse-cu12==12.1.0.106
      - nvidia-nccl-cu12==2.20.5
      - nvidia-nvjitlink-cu12==12.6.68
      - nvidia-nvtx-cu12==12.1.105
      - openpyxl==3.1.5
      - opt-einsum==3.3.0
      - optax==0.2.3
      - orbax==0.1.0
      - orbax-checkpoint==0.6.4
      - packaging==24.1
      - pandas==2.2.3
      - parso==0.8.4
      - patsy==0.5.6
      - pexpect==4.9.0
      - pillow==10.4.0
      - pluggy==1.5.0
      - prompt-toolkit==3.0.47
      - protobuf==5.28.2
      - psutil==6.0.0
      - ptyprocess==0.7.0
      - pure-eval==0.2.3
      - pyarrow==17.0.0
      - pydot==3.0.1
      - pygments==2.18.0
      - pynndescent==0.5.13
      - pyparsing==3.1.4
      - pyro-api==0.1.2
      - pyro-ppl==1.8.6
      - pytest==8.3.3
      - python-dateutil==2.9.0.post0
      - pytorch-lightning==1.9.5
      - pytz==2024.2
      - pyyaml==6.0.2
      - pyzmq==26.2.0
      - regex==2024.9.11
      - requests==2.32.3
      - rich==13.8.1
      - safetensors==0.4.5
      - scanpy==1.10.3
      - scgpt==0.2.1
      - scib==1.1.5
      - scikit-learn==1.5.2
      - scikit-misc==0.5.1
      - scipy==1.14.1
      - scvi-tools==0.20.2
      - seaborn==0.13.2
      - session-info==1.0.0
      - six==1.16.0
      - stack-data==0.6.3
      - statsmodels==0.14.3
      - stdlib-list==0.10.0
      - sympy==1.13.3
      - tensorstore==0.1.65
      - texttable==1.7.0
      - threadpoolctl==3.5.0
      - tokenizers==0.13.3
      - toolz==0.12.1
      - torch==1.13.0
      - torchaudio==0.13.0+cu117
      - torchmetrics==1.4.2
      - torchtext==0.14.0
      - torchvision==0.14.0+cu117
      - tornado==6.4.1
      - tqdm==4.66.5
      - traitlets==5.14.3
      - transformers==4.33.2
      - triton==3.0.0
      - typing-extensions==4.12.2
      - tzdata==2024.2
      - umap-learn==0.5.6
      - urllib3==2.2.3
      - wcwidth==0.2.13
      - wrapt==1.16.0
      - xxhash==3.5.0
      - yarl==1.12.1
      - zipp==3.20.2
prefix: /home00/liss/miniconda3/envs/scgpt_2
```

