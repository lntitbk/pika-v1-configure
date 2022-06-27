"# pika-v1-configure" 
function numberToWords(inpStr) {
    var and = 'and';
    inpStr = inpStr.replace(/[, ]/g, '');
  
    if (parseInt(inpStr) === 0) {
      return 'zero';
    }

    units = [
      '',
      'one',
      'two',
      'three',
      'four',
      'five',
      'six',
      'seven',
      'eight',
      'nine',
      'ten',
      'eleven',
      'twelve',
      'thirteen',
      'fourteen',
      'fifteen',
      'sixteen',
      'seventeen',
      'eighteen',
      'nineteen',
    ];

    tens = [
      '',
      '',
      'twenty',
      'thirty',
      'forty',
      'fifty',
      'sixty',
      'seventy',
      'eighty',
      'ninety',
    ];
  
    scales = [
      '',
      'thousand',
      'million',
      'billion',
      'trillion',
      'quadrillion'
    ];
  
    var start = string.length;
    var chunks = [];
    while (start > 0) {
      end = start;
      chunks.push(string.slice((start = Math.max(0, start - 3)), end));
    }
  
    var chunksLen = chunks.length;
    if (chunksLen > scales.length) {
      return '';
    }
  
    var words = [];
    for (i = 0; i < chunksLen; i++) {
      var chunk = parseInt(chunks[i]);
      var word;
      if (chunk) {
        var ints = chunks[i].split('').reverse().map(parseFloat);

        if (ints[1] === 1) {
          ints[0] += 10;
        }
  
        if ((word = scales[i])) {
          words.push(word);
        }
  
        if ((word = units[ints[0]])) {
          words.push(word);
        }
  
        if ((word = tens[ints[1]])) {
          words.push(word);
        }
  
        if (ints[0] || ints[1]) {
          if (ints[2] || (!i && chunksLen)) {
            words.push(and);
          }
        }
  
        if ((word = units[ints[2]])) {
          words.push(word + ' hundred');
        }
      }
    }

    return words.reverse().join(' ');
  }
