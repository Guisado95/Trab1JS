const elementType = document.getElementById('elementType');
const elementContent = document.getElementById('elementContent');
const elementImage = document.getElementById('elementImage');
const bgColor = document.getElementById('bgColor');
const textColor = document.getElementById('textColor');
const borderStyle = document.getElementById('borderStyle');
const elementSize = document.getElementById('elementSize');
const addElementButton = document.getElementById('addElementButton');
const clearFields = document.getElementById('clearFields');
const headerPreview = document.getElementById('headerPreview');
const headerBgColor = document.getElementById('headerBgColor');

let editingElement = null;

// FUNDO DO CABEÇALHO
headerBgColor.addEventListener('input', () => {
  headerPreview.style.backgroundColor = headerBgColor.value;
});

// IMAGEM OU TEXTO
elementType.addEventListener('change', () => {
  if (elementType.value === 'image') {
    elementContent.classList.add('d-none');
    elementImage.classList.remove('d-none');
  } else {
    elementContent.classList.remove('d-none');
    elementImage.classList.add('d-none');
  }
});

// ADICIONA NOVO ELEMENTO
addElementButton.addEventListener('click', () => {
  if (!editingElement && headerPreview.children.length >= 3) {
    alert('Você só pode adicionar até 3 elementos.');
    return;
  }

  if (elementType.value === 'text' && !elementContent.value.trim()) {
    alert('Digite algum texto para o elemento.');
    return;
  }

  const element = editingElement || document.createElement('div');
  element.classList.add('element-preview');
  element.style.backgroundColor = bgColor.value;
  element.style.border = `2px ${borderStyle.value} black`;
  element.style.width = `${elementSize.value || 200}px`;
  element.style.height = `${elementSize.value || 200}px`;
  element.style.display = 'flex';
  element.style.alignItems = 'center';
  element.style.justifyContent = 'center';
  element.style.color = textColor.value;
  element.innerHTML = ''; 

  if (elementType.value === 'text') {
    const text = document.createElement('p');
    text.textContent = elementContent.value;
    element.appendChild(text);
  } else if (elementType.value === 'image') {
    if (!elementImage.files[0]) {
      alert('Você precisa escolher uma imagem.');
      return;
    }
    const reader = new FileReader();
    reader.onload = function (e) {
      const img = document.createElement('img');
      img.src = e.target.result;
      img.style.maxWidth = '100%';
      img.style.maxHeight = '100%';
      element.appendChild(img);

      // ADICIONA AO DOM
      if (!editingElement) {
        headerPreview.appendChild(element);
        element.addEventListener('click', () => editElement(element));
      }
    };
    reader.readAsDataURL(elementImage.files[0]);
  }

  if (elementType.value === 'text') {
    if (!editingElement) {
      headerPreview.appendChild(element);
      element.addEventListener('click', () => editElement(element));
    }
  }
  editingElement = null;
  resetForm();
});

// LIMPA OS CAMPOS
clearFields.addEventListener('click', () => {
  resetForm();
  headerPreview.innerHTML = '';
  headerPreview.style.backgroundColor = '#ffffff';
});

// RESETA OS INPUTS
function resetForm() {
  elementType.value = 'text';
  elementContent.value = '';
  elementImage.value = '';
  bgColor.value = '#ffffff';
  textColor.value = '#000000';
  borderStyle.value = 'none';
  elementSize.value = '200';
  elementContent.classList.remove('d-none');
  elementImage.classList.add('d-none');
  editingElement = null;
}
