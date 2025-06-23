#perl 

# Perl Nedir?

+ Perl, **"Practical Extraction and Reporting Language"** (Pratik Çıkarma ve Raporlama Dili) veya Larry Wall'un esprili deyimiyle **"Pathologically Eclectic Rubbish Lister"** (Patolojik Derecede Eklektik Çöp Listeleme Dili) olarak bilinen, yüksek seviyeli, dinamik bir programlama dilidir.

# Merhaba Dünya:

**hello_world.pl:**

```perl
#!/usr/bin/perl

# use strict;
# use warnings;

print "Merhaba Dünya";
```

**Perl Çalıştır:**

```shell
perl hello_world.pl    # Çıktı: Merhaba Dünya%
```

# Değişken:

## A. Skalar(scalar) Değişken:

+ Perl'de **skalar değişkenler**, en temel veri türüdür ve **tek bir değer** tutar: bu bir sayı, metin (string), ondalıklı sayı, boolean (mantıksal değer), hatta başka bir skalar olabilir.


> [!NOTE]
> **Skalar (scalar)** değişken, tek bir değeri temsil eder. Aşağıdaki veri türlerinden herhangi biri olabilir:
> + Sayı (integer veya float)
> + Metin (string)
> + Boolean değer (true/false)

### Syntax: