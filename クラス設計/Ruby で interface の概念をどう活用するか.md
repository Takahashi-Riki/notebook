<script>
  alert("Hello world!!");
</script>

# 前提

- Ruby には interface の概念がない。

# 結論

Matz さんに従って、無理に interface を実現するのではなく、interface を意識した実装を行う。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">Rubyでは、型やインターフェースはあなたの心の中にあるのです。<br><br>まあ、抽象クラスやインターフェースの代わりにmoduleが使えますが、使いすぎるとRubyっぽくなくなるので、ほどほどに。</p>&mdash; Yukihiro Matz (@yukihiro_matz) <a href="https://twitter.com/yukihiro_matz/status/1066980158429552640?ref_src=twsrc%5Etfw">November 26, 2018</a></blockquote>

# 検討記録

Ruby で interface の概念を活用する方法としては下記が考えられる。
個人開発でない限り、案2は社内で合意をとって導入する必要があり、かなり現実的でないため、一人の開発者として案1を選ぶのが妥当。

- 案1: interface を意識した実装を行う。
- 案2: interface を何らかの方法で Ruby で実現する。
  - 案2-1: 継承を利用する。
  - 案2-2: module を利用する。 

# サンプルコード

```ruby
class Fire
  attr_reader :member

  def initialize(member)
    @member = member
  end

  def name
    "ファイア"
  end

  def cost_magic_point
    return MagicPoint.new(20)
  end

  def attack_power
    return AttackPower.new(50)
  end

  def cost_technical_point
    return TechnicalPoint.new(0)
  end
end

class Shiden
  attr_reader :member

  def initialize(member)
    @member = member
  end

  def name
    "紫電"
  end

  def cost_magic_point
    return MagicPoint.new(10)
  end

  def attack_power
    return AttackPower.new(30)
  end

  def cost_technical_point
    return TechnicalPoint.new(10)
  end
end

magics = {}
magics[:fire] = Fire.new(member)
magics[:shiden] = Shiden.new(member)

def magic_attack(magic_type)
  using_magic = magics[magic_type]

  # 処理
end
```
