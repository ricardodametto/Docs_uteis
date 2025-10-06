https://g.co/gemini/share/030982dc17ee
Dependencias:

sudo apt update && sudo apt upgrade -y

sudo apt install -y \

sudo \

curl \

wget \

git \

build-essential \

software-properties-common \

ca-certificates \

locales \

unzip \

python3 \

python3-pip \

pkg-config \

cmake \

gnupg2 \

nasm \

gdb \

libncurses5-dev libncursesw5-dev libgtk2.0-dev libatk1.0-dev
libcairo2-dev libx11-dev libxpm-dev libxt-dev liblua5.3-dev lua5.3 nasm
clangd binutils

\# Clonar repositório

git clone https://github.com/vim/vim.git ~/vim

cd ~/vim-git

\# Configurar a build

./configure \\

\--with-features=huge \\

\--enable-multibyte \\

\--enable-python3interp=yes \\

\--enable-cscope \\

\--enable-gui=auto \\

\--enable-gtk2 \\

\--enable-gnome-check \\

\--enable-fontset \\

\--enable-largefile \\

\--enable-terminal \\

\--enable-fail-if-missing \\

\--with-x \\

\--enable-rubyinterp=no \\

\--enable-luainterp=yes \\

\--with-luajit

\# Compilar

make

\# Instalar

make install


./configure \
    --with-features=huge \
    --enable-multibyte \
    --enable-python3interp \
    --with-compiledby="Distrobox Debian Build"
make -j$(nproc) 
make install   
    
vim --version \| head -n 20

Instalar nodejs npm

curl -fsSL https://deb.nodesource.com/setup_20.x | sudo bash -

sudo apt install -y nodejs

node -v

npm -v

Instalar Rust/cargo(necesário para asm-lsp)

curl --proto '=https\' --tlsv1.2 -sSf https://sh.rustup.rs | sh

source $HOME/.cargo/env

rustc --version

cargo --version

Criar diretórios para plugins(Usaremos tudo pelo coc.nvim)

mkdir -p \~/.vim/pack/coc/start

mkdir -p \~/.vim/pack/plugins/start

Instalar coc.nvim

cd ~/.vim/pack/coc/start

git clone \--branch release htttps://github.com/neoclide/coc.nvim.git

Instalar auto-pairs

cd ~/.vim/pack/plugins/start

git clone https://github.com/jiangmiao/auto-pairs.git

Instalar asm-lsp

cargo install asm-lsp

which asm-lsp \# deve retornar \~/.cargo/bin/asm-lsp

Editar *\~/.vim/coc-settings.json*

{

\"languageserver\": {

\"nasm\": {

\"command\": \"/home/ricardo/.cargo/bin/asm-lsp\",

\"filetypes\": \[\"asm\", \"nasm\"\],

\"rootPatterns\": \[\".git/\"\]

}

},

\"java.jdt.ls.java.home\":
**\"/home/ricardo/.config/coc/extensions/coc-java-data/jdk-23.0.2-linux-x64\",**

\"java.jdt.ls.vmargs\": \"-noverify -Xmx1G -XX:+UseG1GC
-XX:+UseStringDeduplication\",

\"coc.preferences.formatOnSaveFiletypes\": \[\"c\", \"asm\", \"java\"\]

}

OBS: java está apontando para o próprio jdk-23.0.2-linux-x64 baixado na
instalação do lsp java feito pelo coc nesse diretorio
**\"/home/ricardo/.config/coc/extensions/coc-java-data/jdk-23.0.2-linux-x64\"**

Abiri o vim e instalar

:CocInstall coc-clangd coc-java coc-nasm

Editar o .vimrc:

\" ===========================================

\" \~/.vimrc -- Configuração final pronta para LSP

\" C, NASM, Java com coc.nvim + plugins

\" ===========================================

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

\" Carregar plugins do pack

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

set rtp+=\~/.vim/pack/plugins/start/auto-pairs

set rtp+=\~/.vim/pack/coc/start/coc.nvim

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

\" Básico

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

set nocompatible \" desativa modo compatível Vi

filetype plugin indent on

syntax on

set number \" mostra números de linha

set relativenumber \" números relativos

set cursorline \" destaca linha atual

set tabstop=4 shiftwidth=4 expandtab

set smartindent

set hidden \" manter buffers abertos

set encoding=utf-8

set termguicolors

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

\" Colorscheme

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

colorscheme elflord

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

\" coc.nvim configuração

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

\" LSP já instalado: coc-clangd, coc-java, coc-nasm

let g:coc_global_extensions = \[\'coc-clangd\', \'coc-java\',
\'coc-nasm\'\]

\" Atalhos úteis coc.nvim

nmap \<silent\> gd \<Plug\>(coc-definition)

nmap \<silent\> gy \<Plug\>(coc-type-definition)

nmap \<silent\> gi \<Plug\>(coc-implementation)

nmap \<silent\> gr \<Plug\>(coc-references)

\" Mostrar documentação rápida

nnoremap K :call CocActionAsync(\'doHover\')\<CR\>

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

\" Autocomplete coc.nvim -- TAB + Enter funcionando corretamente

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

function! s:check_back_space() abort

let col = col(\'.\') - 1

return !col \|\| getline(\'.\')\[col - 1\] =\~# \'\\s\'

endfunction

inoremap \<silent\>\<expr\> \<TAB\>

\\ coc#pum#visible() ? coc#pum#next(1) :

\\ \<SID\>check_back_space() ? \"\\\<TAB\>\" :

\\ coc#refresh()

inoremap \<silent\>\<expr\> \<S-TAB\>

\\ coc#pum#visible() ? coc#pum#prev(1) : \"\\\<C-h\>\"

inoremap \<silent\>\<expr\> \<CR\>

\\ coc#pum#visible() ? coc#pum#confirm() : \"\\\<CR\>\"

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

\" Outras configurações úteis

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

set history=1000

set clipboard=unnamedplus

set incsearch

set ignorecase

set smartcase

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

\" Plugin Auto-pairs

\" \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

\" habilitado automaticamente quando instalado via pack

let g:AutoPairsFlyMode = 1
