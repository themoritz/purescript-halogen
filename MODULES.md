# Module Documentation

## Module Halogen

#### `Heff`

``` purescript
type Heff eff = Eff (dom :: DOM, ref :: Ref | eff)
```

Wraps the effects required by the `runUI` and `runUIEff` functions.

#### `runUI`

``` purescript
runUI :: forall i eff. Signal1 i (HTML i) -> Heff eff Node
```

`runUI` takes a UI represented as a signal function, and renders it to the DOM
using `virtual-dom`.

The signal function is responsible for rendering the HTML for the UI, and the 
HTML can generate inputs which will be fed back into the signal function,
resulting in DOM updates.

This function returns a `Node`, and the caller is responsible for adding the node
to the DOM.

As a simple example, we can create a signal which responds to button clicks:

```purescript
ui :: forall eff. Signal1 eff Unit (HTML Unit)
ui = view <$> stateful 0 (\n _ -> n + 1)
  where
  view :: Number -> HTML Unit
  view n = button [ OnClick (const unit) ] [ text (show n) ]
```


#### `runUIEff`

``` purescript
runUIEff :: forall i r eff. Signal1 i (HTML r) -> (r -> (i -> Heff eff Unit) -> Heff eff Unit) -> Heff eff Node
```

`runUIEff` is a more general version of `runUI` which can be used to construct other
top-level handlers for applications.

`runUIEff` takes a signal function which creates HTML documents containing _requests_, 
and a handler function which accepts requests and provides new inputs to a continuation as they
become available.

For example, the handler function might be responsible for issuing AJAX requests on behalf of the
application.

In this way, all effects are pushed to the handler function at the boundary of the application.



## Module Halogen.HTML

#### `MouseEvent`

``` purescript
data MouseEvent
```


#### `Attribute`

``` purescript
data Attribute i
  = OnClick (MouseEvent -> i)
```

#### `functorAttribute`

``` purescript
instance functorAttribute :: Functor Attribute
```


#### `HTML`

``` purescript
data HTML i
```

The `HTML` type represents HTML documents before being rendered to the virtual DOM, and ultimately,
the actual DOM.

This representation is useful because it supports various typed transformations. It also gives a 
strongly-typed representation for the events which can be generated by a document.

The type parameter `i` represents the type of events which can be generated by this document.

#### `functorHTML`

``` purescript
instance functorHTML :: Functor HTML
```


#### `renderHtml`

``` purescript
renderHtml :: forall i eff. (i -> Eff eff Unit) -> HTML i -> VTree
```

Render a `HTML` document to a virtual DOM node

#### `text`

``` purescript
text :: forall i. String -> HTML i
```


#### `a`

``` purescript
a :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `a_`

``` purescript
a_ :: forall i. [HTML i] -> HTML i
```


#### `abbr`

``` purescript
abbr :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `abbr_`

``` purescript
abbr_ :: forall i. [HTML i] -> HTML i
```


#### `acronym`

``` purescript
acronym :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `acronym_`

``` purescript
acronym_ :: forall i. [HTML i] -> HTML i
```


#### `address`

``` purescript
address :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `address_`

``` purescript
address_ :: forall i. [HTML i] -> HTML i
```


#### `applet`

``` purescript
applet :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `applet_`

``` purescript
applet_ :: forall i. [HTML i] -> HTML i
```


#### `area`

``` purescript
area :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `area_`

``` purescript
area_ :: forall i. [HTML i] -> HTML i
```


#### `article`

``` purescript
article :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `article_`

``` purescript
article_ :: forall i. [HTML i] -> HTML i
```


#### `aside`

``` purescript
aside :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `aside_`

``` purescript
aside_ :: forall i. [HTML i] -> HTML i
```


#### `audio`

``` purescript
audio :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `audio_`

``` purescript
audio_ :: forall i. [HTML i] -> HTML i
```


#### `b`

``` purescript
b :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `b_`

``` purescript
b_ :: forall i. [HTML i] -> HTML i
```


#### `base`

``` purescript
base :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `base_`

``` purescript
base_ :: forall i. [HTML i] -> HTML i
```


#### `basefont`

``` purescript
basefont :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `basefont_`

``` purescript
basefont_ :: forall i. [HTML i] -> HTML i
```


#### `bdi`

``` purescript
bdi :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `bdi_`

``` purescript
bdi_ :: forall i. [HTML i] -> HTML i
```


#### `bdo`

``` purescript
bdo :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `bdo_`

``` purescript
bdo_ :: forall i. [HTML i] -> HTML i
```


#### `big`

``` purescript
big :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `big_`

``` purescript
big_ :: forall i. [HTML i] -> HTML i
```


#### `blockquote`

``` purescript
blockquote :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `blockquote_`

``` purescript
blockquote_ :: forall i. [HTML i] -> HTML i
```


#### `body`

``` purescript
body :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `body_`

``` purescript
body_ :: forall i. [HTML i] -> HTML i
```


#### `br`

``` purescript
br :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `br_`

``` purescript
br_ :: forall i. [HTML i] -> HTML i
```


#### `button`

``` purescript
button :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `button_`

``` purescript
button_ :: forall i. [HTML i] -> HTML i
```


#### `canvas`

``` purescript
canvas :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `canvas_`

``` purescript
canvas_ :: forall i. [HTML i] -> HTML i
```


#### `caption`

``` purescript
caption :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `caption_`

``` purescript
caption_ :: forall i. [HTML i] -> HTML i
```


#### `center`

``` purescript
center :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `center_`

``` purescript
center_ :: forall i. [HTML i] -> HTML i
```


#### `cite`

``` purescript
cite :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `cite_`

``` purescript
cite_ :: forall i. [HTML i] -> HTML i
```


#### `code`

``` purescript
code :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `code_`

``` purescript
code_ :: forall i. [HTML i] -> HTML i
```


#### `col`

``` purescript
col :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `col_`

``` purescript
col_ :: forall i. [HTML i] -> HTML i
```


#### `colgroup`

``` purescript
colgroup :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `colgroup_`

``` purescript
colgroup_ :: forall i. [HTML i] -> HTML i
```


#### `datalist`

``` purescript
datalist :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `datalist_`

``` purescript
datalist_ :: forall i. [HTML i] -> HTML i
```


#### `dd`

``` purescript
dd :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `dd_`

``` purescript
dd_ :: forall i. [HTML i] -> HTML i
```


#### `del`

``` purescript
del :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `del_`

``` purescript
del_ :: forall i. [HTML i] -> HTML i
```


#### `details`

``` purescript
details :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `details_`

``` purescript
details_ :: forall i. [HTML i] -> HTML i
```


#### `dfn`

``` purescript
dfn :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `dfn_`

``` purescript
dfn_ :: forall i. [HTML i] -> HTML i
```


#### `dialog`

``` purescript
dialog :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `dialog_`

``` purescript
dialog_ :: forall i. [HTML i] -> HTML i
```


#### `dir`

``` purescript
dir :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `dir_`

``` purescript
dir_ :: forall i. [HTML i] -> HTML i
```


#### `div`

``` purescript
div :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `div_`

``` purescript
div_ :: forall i. [HTML i] -> HTML i
```


#### `dl`

``` purescript
dl :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `dl_`

``` purescript
dl_ :: forall i. [HTML i] -> HTML i
```


#### `dt`

``` purescript
dt :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `dt_`

``` purescript
dt_ :: forall i. [HTML i] -> HTML i
```


#### `em`

``` purescript
em :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `em_`

``` purescript
em_ :: forall i. [HTML i] -> HTML i
```


#### `embed`

``` purescript
embed :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `embed_`

``` purescript
embed_ :: forall i. [HTML i] -> HTML i
```


#### `fieldset`

``` purescript
fieldset :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `fieldset_`

``` purescript
fieldset_ :: forall i. [HTML i] -> HTML i
```


#### `figcaption`

``` purescript
figcaption :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `figcaption_`

``` purescript
figcaption_ :: forall i. [HTML i] -> HTML i
```


#### `figure`

``` purescript
figure :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `figure_`

``` purescript
figure_ :: forall i. [HTML i] -> HTML i
```


#### `font`

``` purescript
font :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `font_`

``` purescript
font_ :: forall i. [HTML i] -> HTML i
```


#### `footer`

``` purescript
footer :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `footer_`

``` purescript
footer_ :: forall i. [HTML i] -> HTML i
```


#### `form`

``` purescript
form :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `form_`

``` purescript
form_ :: forall i. [HTML i] -> HTML i
```


#### `frame`

``` purescript
frame :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `frame_`

``` purescript
frame_ :: forall i. [HTML i] -> HTML i
```


#### `frameset`

``` purescript
frameset :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `frameset_`

``` purescript
frameset_ :: forall i. [HTML i] -> HTML i
```


#### `h1`

``` purescript
h1 :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `h1_`

``` purescript
h1_ :: forall i. [HTML i] -> HTML i
```


#### `h2`

``` purescript
h2 :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `h2_`

``` purescript
h2_ :: forall i. [HTML i] -> HTML i
```


#### `h3`

``` purescript
h3 :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `h3_`

``` purescript
h3_ :: forall i. [HTML i] -> HTML i
```


#### `h4`

``` purescript
h4 :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `h4_`

``` purescript
h4_ :: forall i. [HTML i] -> HTML i
```


#### `h5`

``` purescript
h5 :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `h5_`

``` purescript
h5_ :: forall i. [HTML i] -> HTML i
```


#### `h6`

``` purescript
h6 :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `h6_`

``` purescript
h6_ :: forall i. [HTML i] -> HTML i
```


#### `head`

``` purescript
head :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `head_`

``` purescript
head_ :: forall i. [HTML i] -> HTML i
```


#### `header`

``` purescript
header :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `header_`

``` purescript
header_ :: forall i. [HTML i] -> HTML i
```


#### `hr`

``` purescript
hr :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `hr_`

``` purescript
hr_ :: forall i. [HTML i] -> HTML i
```


#### `html`

``` purescript
html :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `html_`

``` purescript
html_ :: forall i. [HTML i] -> HTML i
```


#### `i`

``` purescript
i :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `i_`

``` purescript
i_ :: forall i. [HTML i] -> HTML i
```


#### `iframe`

``` purescript
iframe :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `iframe_`

``` purescript
iframe_ :: forall i. [HTML i] -> HTML i
```


#### `img`

``` purescript
img :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `img_`

``` purescript
img_ :: forall i. [HTML i] -> HTML i
```


#### `input`

``` purescript
input :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `input_`

``` purescript
input_ :: forall i. [HTML i] -> HTML i
```


#### `ins`

``` purescript
ins :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `ins_`

``` purescript
ins_ :: forall i. [HTML i] -> HTML i
```


#### `kbd`

``` purescript
kbd :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `kbd_`

``` purescript
kbd_ :: forall i. [HTML i] -> HTML i
```


#### `keygen`

``` purescript
keygen :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `keygen_`

``` purescript
keygen_ :: forall i. [HTML i] -> HTML i
```


#### `label`

``` purescript
label :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `label_`

``` purescript
label_ :: forall i. [HTML i] -> HTML i
```


#### `legend`

``` purescript
legend :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `legend_`

``` purescript
legend_ :: forall i. [HTML i] -> HTML i
```


#### `li`

``` purescript
li :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `li_`

``` purescript
li_ :: forall i. [HTML i] -> HTML i
```


#### `link`

``` purescript
link :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `link_`

``` purescript
link_ :: forall i. [HTML i] -> HTML i
```


#### `main`

``` purescript
main :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `main_`

``` purescript
main_ :: forall i. [HTML i] -> HTML i
```


#### `map`

``` purescript
map :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `map_`

``` purescript
map_ :: forall i. [HTML i] -> HTML i
```


#### `mark`

``` purescript
mark :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `mark_`

``` purescript
mark_ :: forall i. [HTML i] -> HTML i
```


#### `menu`

``` purescript
menu :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `menu_`

``` purescript
menu_ :: forall i. [HTML i] -> HTML i
```


#### `menuitem`

``` purescript
menuitem :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `menuitem_`

``` purescript
menuitem_ :: forall i. [HTML i] -> HTML i
```


#### `meta`

``` purescript
meta :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `meta_`

``` purescript
meta_ :: forall i. [HTML i] -> HTML i
```


#### `meter`

``` purescript
meter :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `meter_`

``` purescript
meter_ :: forall i. [HTML i] -> HTML i
```


#### `nav`

``` purescript
nav :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `nav_`

``` purescript
nav_ :: forall i. [HTML i] -> HTML i
```


#### `noframes`

``` purescript
noframes :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `noframes_`

``` purescript
noframes_ :: forall i. [HTML i] -> HTML i
```


#### `noscript`

``` purescript
noscript :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `noscript_`

``` purescript
noscript_ :: forall i. [HTML i] -> HTML i
```


#### `object`

``` purescript
object :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `object_`

``` purescript
object_ :: forall i. [HTML i] -> HTML i
```


#### `ol`

``` purescript
ol :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `ol_`

``` purescript
ol_ :: forall i. [HTML i] -> HTML i
```


#### `optgroup`

``` purescript
optgroup :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `optgroup_`

``` purescript
optgroup_ :: forall i. [HTML i] -> HTML i
```


#### `option`

``` purescript
option :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `option_`

``` purescript
option_ :: forall i. [HTML i] -> HTML i
```


#### `output`

``` purescript
output :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `output_`

``` purescript
output_ :: forall i. [HTML i] -> HTML i
```


#### `p`

``` purescript
p :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `p_`

``` purescript
p_ :: forall i. [HTML i] -> HTML i
```


#### `param`

``` purescript
param :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `param_`

``` purescript
param_ :: forall i. [HTML i] -> HTML i
```


#### `pre`

``` purescript
pre :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `pre_`

``` purescript
pre_ :: forall i. [HTML i] -> HTML i
```


#### `progress`

``` purescript
progress :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `progress_`

``` purescript
progress_ :: forall i. [HTML i] -> HTML i
```


#### `q`

``` purescript
q :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `q_`

``` purescript
q_ :: forall i. [HTML i] -> HTML i
```


#### `rp`

``` purescript
rp :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `rp_`

``` purescript
rp_ :: forall i. [HTML i] -> HTML i
```


#### `rt`

``` purescript
rt :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `rt_`

``` purescript
rt_ :: forall i. [HTML i] -> HTML i
```


#### `ruby`

``` purescript
ruby :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `ruby_`

``` purescript
ruby_ :: forall i. [HTML i] -> HTML i
```


#### `s`

``` purescript
s :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `s_`

``` purescript
s_ :: forall i. [HTML i] -> HTML i
```


#### `samp`

``` purescript
samp :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `samp_`

``` purescript
samp_ :: forall i. [HTML i] -> HTML i
```


#### `script`

``` purescript
script :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `script_`

``` purescript
script_ :: forall i. [HTML i] -> HTML i
```


#### `section`

``` purescript
section :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `section_`

``` purescript
section_ :: forall i. [HTML i] -> HTML i
```


#### `select`

``` purescript
select :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `select_`

``` purescript
select_ :: forall i. [HTML i] -> HTML i
```


#### `small`

``` purescript
small :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `small_`

``` purescript
small_ :: forall i. [HTML i] -> HTML i
```


#### `source`

``` purescript
source :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `source_`

``` purescript
source_ :: forall i. [HTML i] -> HTML i
```


#### `span`

``` purescript
span :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `span_`

``` purescript
span_ :: forall i. [HTML i] -> HTML i
```


#### `strike`

``` purescript
strike :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `strike_`

``` purescript
strike_ :: forall i. [HTML i] -> HTML i
```


#### `strong`

``` purescript
strong :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `strong_`

``` purescript
strong_ :: forall i. [HTML i] -> HTML i
```


#### `style`

``` purescript
style :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `style_`

``` purescript
style_ :: forall i. [HTML i] -> HTML i
```


#### `sub`

``` purescript
sub :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `sub_`

``` purescript
sub_ :: forall i. [HTML i] -> HTML i
```


#### `summary`

``` purescript
summary :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `summary_`

``` purescript
summary_ :: forall i. [HTML i] -> HTML i
```


#### `sup`

``` purescript
sup :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `sup_`

``` purescript
sup_ :: forall i. [HTML i] -> HTML i
```


#### `table`

``` purescript
table :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `table_`

``` purescript
table_ :: forall i. [HTML i] -> HTML i
```


#### `tbody`

``` purescript
tbody :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `tbody_`

``` purescript
tbody_ :: forall i. [HTML i] -> HTML i
```


#### `td`

``` purescript
td :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `td_`

``` purescript
td_ :: forall i. [HTML i] -> HTML i
```


#### `textarea`

``` purescript
textarea :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `textarea_`

``` purescript
textarea_ :: forall i. [HTML i] -> HTML i
```


#### `tfoot`

``` purescript
tfoot :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `tfoot_`

``` purescript
tfoot_ :: forall i. [HTML i] -> HTML i
```


#### `th`

``` purescript
th :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `th_`

``` purescript
th_ :: forall i. [HTML i] -> HTML i
```


#### `thead`

``` purescript
thead :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `thead_`

``` purescript
thead_ :: forall i. [HTML i] -> HTML i
```


#### `time`

``` purescript
time :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `time_`

``` purescript
time_ :: forall i. [HTML i] -> HTML i
```


#### `title`

``` purescript
title :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `title_`

``` purescript
title_ :: forall i. [HTML i] -> HTML i
```


#### `tr`

``` purescript
tr :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `tr_`

``` purescript
tr_ :: forall i. [HTML i] -> HTML i
```


#### `track`

``` purescript
track :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `track_`

``` purescript
track_ :: forall i. [HTML i] -> HTML i
```


#### `tt`

``` purescript
tt :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `tt_`

``` purescript
tt_ :: forall i. [HTML i] -> HTML i
```


#### `u`

``` purescript
u :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `u_`

``` purescript
u_ :: forall i. [HTML i] -> HTML i
```


#### `ul`

``` purescript
ul :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `ul_`

``` purescript
ul_ :: forall i. [HTML i] -> HTML i
```


#### `var`

``` purescript
var :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `var_`

``` purescript
var_ :: forall i. [HTML i] -> HTML i
```


#### `video`

``` purescript
video :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `video_`

``` purescript
video_ :: forall i. [HTML i] -> HTML i
```


#### `wbr`

``` purescript
wbr :: forall i. [Attribute i] -> [HTML i] -> HTML i
```


#### `wbr_`

``` purescript
wbr_ :: forall i. [HTML i] -> HTML i
```



## Module Halogen.Signal

#### `Signal`

``` purescript
newtype Signal i o
```

A `Signal` represents a state machine which responds to inputs of type `i`, producing outputs of type `o`.

#### `runSignal`

``` purescript
runSignal :: forall i o. Signal i o -> i -> Signal1 i o
```

Run a `Signal` by providing an input

#### `Signal1`

``` purescript
newtype Signal1 i o
```

`Signal1` represents non-empty signals, i.e. signals with an initial output value.

#### `runSignal1`

``` purescript
runSignal1 :: forall i o. Signal1 i o -> { next :: Signal i o, result :: o }
```

Run a `Signal1` to obtain the initial value and remaining signal

#### `input`

``` purescript
input :: forall i. Signal i i
```

A `Signal` which returns the latest input

#### `startingAt`

``` purescript
startingAt :: forall i o. Signal i o -> o -> Signal1 i o
```

Convert a `Signal` to a `Signal1` by providing an initial value

#### `head`

``` purescript
head :: forall i o. Signal1 i o -> o
```

Get the current value of a `Signal1`

#### `tail`

``` purescript
tail :: forall i o. Signal1 i o -> Signal i o
```

Convert a `Signal1` to a `Signal` by ignoring its initial value

#### `stateful`

``` purescript
stateful :: forall s i o. s -> (s -> i -> s) -> Signal1 i s
```

Creates a stateful `Signal`

#### `functorSignal`

``` purescript
instance functorSignal :: Functor (Signal i)
```


#### `functorSignal1`

``` purescript
instance functorSignal1 :: Functor (Signal1 i)
```


#### `applySignal`

``` purescript
instance applySignal :: Apply (Signal i)
```


#### `applySignal1`

``` purescript
instance applySignal1 :: Apply (Signal1 i)
```


#### `applicativeSignal`

``` purescript
instance applicativeSignal :: Applicative (Signal i)
```


#### `applicativeSignal1`

``` purescript
instance applicativeSignal1 :: Applicative (Signal1 i)
```


#### `profunctorSignal`

``` purescript
instance profunctorSignal :: Profunctor Signal
```


#### `profunctorSignal1`

``` purescript
instance profunctorSignal1 :: Profunctor Signal1
```


#### `semigroupoidSignal`

``` purescript
instance semigroupoidSignal :: Semigroupoid Signal
```


#### `semigroupoidSignal1`

``` purescript
instance semigroupoidSignal1 :: Semigroupoid Signal1
```


#### `categorySignal`

``` purescript
instance categorySignal :: Category Signal
```



