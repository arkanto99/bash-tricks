# bash-tricks

### Seleccionar un directorio temporal para descargar con pip

Al descargar paquetes con pip, si el directorio raiz del sistema está muy lleno, la descarga puede verse interrumpida por no haber espacio disponible. Esto vine provocado porque aunque exista espacio disponible en el disco donde se intenten descargar, en el proceso se crean copias temporales en el raiz que provocan este error.

Esto puede solucionarse facilmente indicando un directorio temporal que ejerza de raiz durante la descarga:
```bash
TMPDIR=/home/pablo/tmp_pip python -m pip download transformers evaluate numpy tensorboard wheel datasets tokenizers torch torchvision nvidia-ml-py einops accuracy "spacy<3.8" ms3 music21 tqdm pandas seaborn plotly matplotlib --extra-index-url https://download.pytorch.org/whl/cu126
```
 ### Eliminar copias desactualizadas de paquetes snap
 ```bash
sudo snap list --all | awk '/desactivado/{print $1, $3}' | while read snapname revision; do
  sudo snap remove "$snapname" --revision="$revision"
done
```
### Instalar pytorch sin dependencias de CUDA (solo CPU)
Útil para ejecutar scripts con dependencias de torch pero que no es necesario cargar en la GPU.
```bash
pip install torch --index-url https://download.pytorch.org/whl/cpu
```
