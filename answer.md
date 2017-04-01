# April Fools' GTF answer for unsolved problems

## Illustration Shop (Stego,Guess 257pts)
First, you can get a image file. This file has other images. You can extract 4 images from this.
The flag is divided and hidden in these images using following stego tools.

[steghide](http://steghide.sourceforge.net/)
[stepic](http://domnit.org/stepic/doc/)
[LSB-Steganography](https://github.com/RobinDavid/LSB-Steganography)
[steganography](http://qiita.com/haminiku/items/2e623caab751f25a382e)

```
% steghide extract -sf ./1.jpg
Enter passphrase:[ENTER]
wrote extracted data to "flag1".

% cat flag1
TWGTF{7h
```

```
% stepic -d -i ./2.png 
3r3_4r3_
```

```
% python lsb.py -steg-image ./3.png -out flag3

% cat flag3
4_l07_0f
```

```
% steganography -d ./4.png 
_Stegano
```

```
% xxd ./flag.png
(snip)
0003b300: 8888 8888 e83f e7af 88f2 f823 b381 c576  .....?.....#...v
0003b310: 0000 0000 4945 4e44 ae42 6082 6772 6170  ....IEND.B`.grap
0003b320: 6879 5f37 3030 6c35 7dff d8ff e000 104a  hy_700l5}......J
0003b330: 4649 4600 0101 0000 0100 0100 00ff db00  FIF.............
(snip)
-> graphy_700l5}
```

TWGTF{7h3r3_4r3_4_l07_0f_Steganography_700l5}



## Grypted Picture (Guess Grypt 255pts)
JPEG encoded with 8-bit gray code



## happeace (Guess Grypto 333pts)
Add `def eval(a); p a; end;` to the top of source code, then you can deobfuscate the source code 
```ruby
def mp(n, m, p)
  r = 1
  while m > 0
    r = r * n % p if (m & 1) != 0
    n = n * n
    m >>= 1
  end
  return r
end

p, q = ARGV[0].to_i(16), ARGV[1].to_i(16)
e = 65537
fail if (p * q).gcd(e) != 1
flag = File.read('flag.txt').unpack1("H*").to_i(16)
while flag * 256 < p * q
  flag = flag * 256 + rand(256)
end
flag = flag * 3 % (p * q)

File.write("flag.enc", [(p * q).to_s.reverse, mp(flag, e, p * q).to_s.reverse]*"\n")
```
This is simple RSA encryption program. The public key is `27584244764354155600648132819557552425739308911053695468526968667034154323890864994134663497833719592115504382599703439971159691892334079575950404443602011446419336838856217871035340130932411874730384556226187585284602489506430910226260180660548868167768948231038124272206657956101663093940178036514598668459344791285173861516336695686519246803293235816673540674607123314970280437901456591138028008746827478792461922269717779112571552627646995537762449461611146365164885397581756696407971821937828304533685809925763247979349076965356455212307688361581367086510870101324402293988628902207909120880013129431859816631123, 65537`.

By the way, the public key in ternary numeral is `22222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222202001011011220101210202012210121221012121111020221110200211101120001222120202021202120121122102001012112201120010222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222201121000101121020122010002211002211102001201201022020202102022102202201101001121202200012110210202201221011110110112121121101112002000121011211002111120021102120122210112102221112222002200222112222122222212121001`.
Therefore you can factorize it.

`p=2050432750646101840391335469287879831815929805207852325995359027954469191794671743381261857048287973447131401026859779976760361654132110042100718063313345003389199564626024544433362323405271383895980841575215010259255471211755594963857860786236149381102564556177117319882658704029095649452388565343997456373`



## test problem (flag 2) (Guess 250pts)
 * you can guess that 404 error page is written manually
     * in `The requested URL was not found on this server.`, the path is missing
 * the error page says that is running on `Apache/2.4.18 (Ubuntu)`
     * but today is April Fools' day. Server header told us that is running on `Apache/2.4.10 (Debian)`.
 * so next thing that you have to guess is accessing `/~debian` and you'll see Index.
 * what is toppage's content? that is [History of PHP](http://php.net/manual/en/history.php.php).
     * then you have to guess `.php_history`.
 * so flag 2 is at `/~debian/.php_history`.




## Guess The Flag (Wave 150pts)
Timing Attack.
```php
<!doctype html>
<html lang="ja">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Guess The Flag</title>
    <link rel="stylesheet" href="/assets/css/pure-min.css" integrity="sha384-UQiGfs9ICog+LwheBSRCt1o5cbyKIHbwjWscjemyBMT9YCUMZffs6UqUTd0hObXD">
    <link rel="stylesheet" href="/assets/css/style.css">
  </head>
  <body>
  <?php
    if(empty($_POST['flag'])) {
  ?>
    <div class="main">
      <h1>What's the Flag?</h1>
      <form class="pure-form" method="POST">
        <div class="pure-control-group">
          <input name="flag" type="text" placeholder="Flag" class="pure-input-1">
        </div>
        <button type="submit" class="pure-button pure-button-primary">Guess!!</button>
      </form>
    </div>
  <?php
    } else {
      $flag = getenv('FLAG');
      $correct = true;
      for($i = 0; $i < strlen($flag); $i++) {
        if($flag[$i] == $_POST['flag'][$i]) {
          sleep(1); // Please guess it.
        } else {
          $correct = false;
          break;
        }
      }
      if($correct) {
        echo '<div class="main"><h1>Correct!</h1></div>';
      } else {
        echo '<div class="main"><h1>Wrong</h1></div>';
      }
    }
    ?>
  </body>
</html>
```
You can  the source code for example 

## Impossible (0day 10000 pts)
Please let us know secretly :)


## EoP (Grypto Guess 89pts)
https://en.wikipedia.org/wiki/Menuet_sur_le_nom_d'Haydn_(Ravel)

Table(in Japanese): https://ja.wikipedia.org/wiki/ハイドンの名によるメヌエット 


## Stegoshka (Stego 256pts)
This is very simple steg. The hiddden data is written as each pixel in RGBA order.  
And this image include other steg image recursively.
```python
from PIL import Image
import os

def extractsteg(data):
    open('tmp.png', 'w').write(data)
    img = Image.open('tmp.png')
    return img.tobytes()

data = open('./prob.png').read()
cnt = 2017
while cnt>0:
    data = extractsteg(data)
    open('hoge.png', 'w').write(data)
    if cnt == 895:
        open('fuga.png', 'w').write(data)
    cnt -= 1
```
note that the flag is hidden in the picture which appears in the middle of all nested steg files. Don't miss it.  
The flag is written as exifdata of the image.

## two dimensions (Misc, Guess 225pts)

![](https://i.imgur.com/tgbDcwW.png)

## nazonazo (Guess,Trivia 0pts)
パンはパンでも食べられないパンはな〜んだ？
A. カビたパン

You should not try this challenge. It is a waste of time because the point of "nazonazo" is 0pts.



