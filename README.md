# -study---table-allCheck--vanillaJS-jquery

## table allCheck VanilaJs & Jquery study


### JQUERY
```javascript

$('#allCheck').on('change', function () {
    const tableCheckbox = $(this).closest('table').find('tbody input[type="checkbox"]');
    if ($(this).is(':checked')) {
        tableCheckbox.prop('checked', true);
    } else {
        tableCheckbox.prop('checked', false);
    }
});
$('#mainTable').on('click', 'tr td:not(:first-child)', function () {
    const $tdCheck = $(this).closest('tr').find('td input[type="checkbox"]');
    if ($tdCheck.is(':checked')) {
        $tdCheck.prop('checked', false).trigger('change');
    } else {
        $tdCheck.prop('checked', true).trigger('change');
    }
});
$('#mainTable').on('change', 'tr td', function () {
    const allLength = $('#mainTable tr td input[type="checkbox"]').length;
    const checkedLength = $('#mainTable tr td input[type="checkbox"]:checked').length;
    if (allLength == checkedLength) {
        $('#allCheck').prop('checked', true);
    } else {
        $('#allCheck').prop('checked', false);
    }
});

```


### VANILA JS
```javascript

//checkbox
const allCheck = document.querySelector('#allCheck');
allCheck.addEventListener('change', function (e) {
    const tableCheckbox = this.closest('table').querySelectorAll('tbody input[type="checkbox"]');
    tableCheckbox.forEach(element => {
        if (e.target.checked) {
            element.checked = true;
        } else {
            element.checked = false;
        }
    });
});

const mainTable = document.querySelector('#mainTable');
mainTable.addEventListener('click', function (e) {
    if (e.target.localName != 'td') { return }

    const tdCheck = e.target.closest('tr').querySelector('td input[type="checkbox"]');
    if (tdCheck.checked) {
        tdCheck.checked = false;
    } else {
        tdCheck.checked = true;
    }

    // tdCheck.dispatchEvent(new Event("change"));  -> 이벤트를 걸어주는 js..
    //tdCheck에 이벤트를 걸고 아래 tdcheck에 change을 걸고 체크하고싶으나(jquery처럼 )
    //tdCheck가 비동기로 생기는거라 mainTable에 change을 걸고 e.target을 찾아도 input이 change될때를 감지하지 못함
    //->> 그래서 다른방법으로 change trigger을 넣어주는 대신 changeCheckboxInit() 을 따로 두번씩.. 해주기..
    changeCheckboxInit();
});
mainTable.addEventListener('change', function (e) {
    if (e.target.localName == 'input') {
        changeCheckboxInit();
    }
});

function changeCheckboxInit() {
    const allLength = document.querySelectorAll('#mainTable tr td input[type="checkbox"]').length;
    const checkedLength = document.querySelectorAll('#mainTable tr td input[type="checkbox"]:checked').length;

    if (allLength == checkedLength) {
        allCheck.checked = true;
    } else {
        allCheck.checked = false;
    }
}

```
