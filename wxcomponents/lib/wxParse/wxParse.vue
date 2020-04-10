<template>
<uni-shadow-root class="lib-wxParse-wxParse"><template name="wxParseVideo">
  
  <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
    <video :class="(item.classStr)+' wxParse-'+(item.tag)+'-video'" :src="item.attr.src"></video>
  </view>
</template>

<template name="wxParseImg">
  <image :class="(item.classStr)+' wxParse-'+(item.tag)" :data-from="item.from" :data-src="item.attr.src" :data-idx="item.imgIndex" :src="item.attr.src" mode="aspectFit" @load="wxParseImgLoad" @click="wxParseImgTap" :style="'width:'+(item.width)+'px;'"></image>
</template>

<template name="WxEmojiView">
  <view class="WxEmojiView wxParse-inline" :style="item.styleStr">
    <block v-for="(item,index) in (item.textArray)">
      <block :class="item.text == '\\n' ? 'wxParse-hide':''" v-if="item.node == 'text'">{{item.text}}</block>
      <block v-else-if="item.node == 'element'">
        <image class="wxEmoji" :src="(item.baseSrc)+(item.text)"></image>
      </block>
    </block>
  </view>
</template>

<template name="WxParseBr">
  <text>\n</text>
</template>


<template name="wxParse">
  <block v-for="(item,index) in (wxParseData)">
    <template is="wxParse0" :data="item"></template>
  </block>
</template>



<template name="wxParse0">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse1" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse1" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse1" :data="item"></template>
        </block>
      </view>
    </block>
    <block v-else-if="item.tag == 'table'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse1" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse1" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse1" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template>




<template name="wxParse1">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse2" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse2" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse2" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse2" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse2" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template>



<template name="wxParse2">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse3" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse3" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse3" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse3" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse3" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template>


<template name="wxParse3">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse4" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse4" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse4" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse4" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse4" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template>


<template name="wxParse4">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse5" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse5" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse5" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse5" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse5" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template>


<template name="wxParse5">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse6" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse6" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse6" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse6" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse6" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template>


<template name="wxParse6">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse7" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse7" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse7" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse7" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse7" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template>

<template name="wxParse7">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse8" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse8" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse8" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse8" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse8" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template>


<template name="wxParse8">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse9" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse9" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse9" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse9" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse9" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template>


<template name="wxParse9">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse10" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse10" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse10" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse10" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse10" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template>


<template name="wxParse10">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse11" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse11" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse11" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse11" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse11" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template>


<template name="wxParse11">
  
  
  <block v-if="item.node == 'element'">
    <block v-if="item.tag == 'button'">
      <button type="default" size="mini">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse12" :data="item"></template>
        </block>
      </button>
    </block>
    
    <block v-else-if="item.tag == 'li'">
      <view :class="(item.classStr)+' wxParse-li'" :style="item.styleStr">
        <view :class="(item.classStr)+' wxParse-li-inner'">
          <view :class="(item.classStr)+' wxParse-li-text'">
            <view :class="(item.classStr)+' wxParse-li-circle'"></view>
          </view>
          <view :class="(item.classStr)+' wxParse-li-text'">
            <block v-for="(item,index) in (item.nodes)">
              <template is="wxParse12" :data="item"></template>
            </block>
          </view>
        </view>
      </view>
    </block>

    
    <block v-else-if="item.tag == 'video'">
      <template is="wxParseVideo" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'img'">
      <template is="wxParseImg" :data="item"></template>
    </block>

    
    <block v-else-if="item.tag == 'a'">
      <view @click="wxParseTagATap" :class="'wxParse-inline '+(item.classStr)+' wxParse-'+(item.tag)" :data-src="item.attr.href" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse12" :data="item"></template>
        </block>
      </view>
    </block>

    <block v-else-if="item.tag == 'br'">
      <template is="WxParseBr"></template>
    </block>
    
    <block v-else-if="item.tagType == 'block'">
      <view :class="(item.classStr)+' wxParse-'+(item.tag)" :style="item.styleStr">
        <block v-for="(item,index) in (item.nodes)">
          <template is="wxParse12" :data="item"></template>
        </block>
      </view>
    </block>

    
    <view v-else :class="(item.classStr)+' wxParse-'+(item.tag)+' wxParse-'+(item.tagType)" :style="item.styleStr">
      <block v-for="(item,index) in (item.nodes)">
        <template is="wxParse12" :data="item"></template>
      </block>
    </view>

  </block>

  
  <block v-else-if="item.node == 'text'">
    
    <template is="WxEmojiView" :data="item"></template>
  </block>

</template></uni-shadow-root>
</template>

<script>

global['__wxRoute'] = 'lib/wxParse/wxParse'
/**
 * author: Di (微信小程序开发工程师)
 * organization: WeAppDev(微信小程序开发论坛)(http://weappdev.com)
 *               垂直微信小程序开发交流社区
 * 
 * github地址: https://github.com/icindy/wxParse
 * 
 * for: 微信小程序富文本解析
 * detail : http://weappdev.com/t/wxparse-alpha0-1-html-markdown/184
 */

/**
 * utils函数引入
 **/
import showdown from './showdown.js';
import HtmlToJson from './html2json.js';
/**
 * 配置及公有属性
 **/
var realWindowWidth = 0;
var realWindowHeight = 0;
wx.getSystemInfo({
  success: function (res) {
    realWindowWidth = res.windowWidth
    realWindowHeight = res.windowHeight
  }
})
/**
 * 主函数入口区
 **/
function wxParse(bindName = 'wxParseData', type='html', data='<div class="color:red;">数据不能为空</div>', target,imagePadding) {
  var that = target;
  var transData = {};//存放转化后的数据
  if (type == 'html') {
    transData = HtmlToJson.html2json(data, bindName);
    console.log(JSON.stringify(transData, ' ', ' '));
  } else if (type == 'md' || type == 'markdown') {
    var converter = new showdown.Converter();
    var html = converter.makeHtml(data);
    transData = HtmlToJson.html2json(html, bindName);
    console.log(JSON.stringify(transData, ' ', ' '));
  }
  transData.view = {};
  transData.view.imagePadding = 0;
  if(typeof(imagePadding) != 'undefined'){
    transData.view.imagePadding = imagePadding
  }
  var bindData = {};
  bindData[bindName] = transData;
  that.setData(bindData)
  that.wxParseImgLoad = wxParseImgLoad;
  that.wxParseImgTap = wxParseImgTap;
}
// 图片点击事件
function wxParseImgTap(e) {
  var that = this;
  var nowImgUrl = e.target.dataset.src;
  var tagFrom = e.target.dataset.from;
  if (typeof (tagFrom) != 'undefined' && tagFrom.length > 0) {
    wx.previewImage({
      current: nowImgUrl, // 当前显示图片的http链接
      urls: that.data[tagFrom].imageUrls // 需要预览的图片http链接列表
    })
  }
}

/**
 * 图片视觉宽高计算函数区 
 **/
function wxParseImgLoad(e) {
  var that = this;
  var tagFrom = e.target.dataset.from;
  var idx = e.target.dataset.idx;
  if (typeof (tagFrom) != 'undefined' && tagFrom.length > 0) {
    calMoreImageInfo(e, idx, that, tagFrom)
  } 
}
// 假循环获取计算图片视觉最佳宽高
function calMoreImageInfo(e, idx, that, bindName) {
  var temData = that.data[bindName];
  if (!temData || temData.images.length == 0) {
    return;
  }
  var temImages = temData.images;
  //因为无法获取view宽度 需要自定义padding进行计算，稍后处理
  var recal = wxAutoImageCal(e.detail.width, e.detail.height,that,bindName); 
  // temImages[idx].width = recal.imageWidth;
  // temImages[idx].height = recal.imageheight; 
  // temData.images = temImages;
  // var bindData = {};
  // bindData[bindName] = temData;
  // that.setData(bindData);
  var index = temImages[idx].index
  var key = `${bindName}`
  for (var i of index.split('.')) key+=`.nodes[${i}]`
  var keyW = key + '.width'
  var keyH = key + '.height'
  that.setData({
    [keyW]: recal.imageWidth,
    [keyH]: recal.imageheight,
  })
}

// 计算视觉优先的图片宽高
function wxAutoImageCal(originalWidth, originalHeight,that,bindName) {
  //获取图片的原始长宽
  var windowWidth = 0, windowHeight = 0;
  var autoWidth = 0, autoHeight = 0;
  var results = {};
  var padding = that.data[bindName].view.imagePadding;
  windowWidth = realWindowWidth-2*padding;
  windowHeight = realWindowHeight;
  //判断按照那种方式进行缩放
  // console.log("windowWidth" + windowWidth);
  if (originalWidth > windowWidth) {//在图片width大于手机屏幕width时候
    autoWidth = windowWidth;
    // console.log("autoWidth" + autoWidth);
    autoHeight = (autoWidth * originalHeight) / originalWidth;
    // console.log("autoHeight" + autoHeight);
    results.imageWidth = autoWidth;
    results.imageheight = autoHeight;
  } else {//否则展示原来的数据
    results.imageWidth = originalWidth;
    results.imageheight = originalHeight;
  }
  return results;
}

function wxParseTemArray(temArrayName,bindNameReg,total,that){
  var array = [];
  var temData = that.data;
  var obj = null;
  for(var i = 0; i < total; i++){
    var simArr = temData[bindNameReg+i].nodes;
    array.push(simArr);
  }

  temArrayName = temArrayName || 'wxParseTemArray';
  obj = JSON.parse('{"'+ temArrayName +'":""}');
  obj[temArrayName] = array;
  that.setData(obj);
}

/**
 * 配置emojis
 * 
 */

function emojisInit(reg='',baseSrc="/wxParse/emojis/",emojis){
   HtmlToJson.emojisInit(reg,baseSrc,emojis);
}

module.exports = {
  wxParse: wxParse,
  wxParseTemArray:wxParseTemArray,
  emojisInit:emojisInit
}
export default global['__wxComponents']['lib/wxParse/wxParse']
</script>
<style platform="mp-weixin">
/**
 * author: Di (微信小程序开发工程师)
 * organization: WeAppDev(微信小程序开发论坛)(http://weappdev.com)
 *               垂直微信小程序开发交流社区
 * 
 * github地址: https://github.com/icindy/wxParse
 * 
 * for: 微信小程序富文本解析
 * detail : http://weappdev.com/t/wxparse-alpha0-1-html-markdown/184
 */

.wxParse{
    margin: 0 5px;
    font-family: Helvetica,sans-serif;
    font-size: 28rpx;
    color: #666;
    line-height: 1.8;
}
view{
    word-break:break-all; overflow:auto;
}
.wxParse-inline{
    display: inline;
    margin: 0;
    padding: 0;
}
/*//标题 */
.wxParse-div{margin: 0;padding: 0;}
.wxParse-h1{ font-size:2em; margin: .67em 0 }
.wxParse-h2{ font-size:1.5em; margin: .75em 0 }
.wxParse-h3{ font-size:1.17em; margin: .83em 0 }
.wxParse-h4{ margin: 1.12em 0}
.wxParse-h5 { font-size:.83em; margin: 1.5em 0 }
.wxParse-h6{ font-size:.75em; margin: 1.67em 0 }

.wxParse-h1 {
  font-size: 18px;
  font-weight: 400;
  margin-bottom: .9em;
}
.wxParse-h2 {
  font-size: 16px;
  font-weight: 400;
  margin-bottom: .34em;
}
.wxParse-h3 {
  font-weight: 400;
  font-size: 15px;
  margin-bottom: .34em;
}
.wxParse-h4 {
  font-weight: 400;
  font-size: 14px;
  margin-bottom: .24em;
}
.wxParse-h5 {
  font-weight: 400;
  font-size: 13px;
  margin-bottom: .14em;
}
.wxParse-h6 {
  font-weight: 400;
  font-size: 12px;
  margin-bottom: .04em;
}

.wxParse-h1, .wxParse-h2, .wxParse-h3, .wxParse-h4, .wxParse-h5, .wxParse-h6, .wxParse-b, .wxParse-strong  { font-weight: bolder }

.wxParse-i,.wxParse-cite,.wxParse-em,.wxParse-var,.wxParse-address{font-style:italic}
.wxParse-pre,.wxParse-tt,.wxParse-code,.wxParse-kbd,.wxParse-samp{font-family:monospace}
.wxParse-pre{white-space:pre}
.wxParse-big{font-size:1.17em}
.wxParse-small,.wxParse-sub,.wxParse-sup{font-size:.83em}
.wxParse-sub{vertical-align:sub}
.wxParse-sup{vertical-align:super}
.wxParse-s,.wxParse-strike,.wxParse-del{text-decoration:line-through}
/*wxparse-自定义个性化的css样式*/
/*增加video的css样式*/
.wxParse-strong,.wxParse-s{display: inline}
.wxParse-a{
    color: deepskyblue;
    word-break:break-all;
    overflow:auto;
}

.wxParse-video{
    text-align: center;
    margin: 10px 0;
}

.wxParse-video-video{
    width:100%;
}

.wxParse-img{
    /*background-color: #efefef;*/
    overflow: hidden;
}

.wxParse-blockquote {
    margin: 0;
    padding:10px 0 10px 5px;
    font-family:Courier, Calibri,"宋体";
    background:#f5f5f5;
    border-left: 3px solid #dbdbdb;
}

.wxParse-code,.wxParse-wxxxcode-style{
    display: inline;
    background:#f5f5f5;
}
.wxParse-ul{
    margin: 20rpx 10rpx;
}

.wxParse-li,.wxParse-li-inner{
    display: flex;
    align-items: baseline;
    margin: 10rpx 0;
}
.wxParse-li-text{
    
    align-items: center;
    line-height: 20px;
}

.wxParse-li-circle{
    display: inline-flex;
    width: 5px;
    height: 5px;
    background-color: #333;
    margin-right: 5px;
}

.wxParse-li-square{
    display: inline-flex;
    width: 10rpx;
    height: 10rpx;
    background-color: #333;
    margin-right: 5px;
}
.wxParse-li-ring{
    display: inline-flex;
    width: 10rpx;
    height: 10rpx;
    border: 2rpx solid #333;
    border-radius: 50%;
    background-color: #fff;
    margin-right: 5px;
}

/*.wxParse-table{
    width: 100%;
    height: 400px;
}
.wxParse-thead,.wxParse-tfoot,.wxParse-tr{
    display: flex;
    flex-direction: row;
}
.wxParse-th,.wxParse-td{
    display: flex;
    width: 580px;
    overflow: auto;
}*/

.wxParse-u {
  text-decoration: underline;
}
.wxParse-hide{
    display: none;
}
.WxEmojiView{
    align-items: center;
}
.wxEmoji{
    width: 16px;
    height:16px;
}
.wxParse-tr{
	display: flex;
	border-right:1px solid #e0e0e0;
	border-bottom:1px solid #e0e0e0;
	border-top:1px solid #e0e0e0;
}
.wxParse-th,
.wxParse-td{
	flex:1;
	padding:5px;
	font-size:28rpx;
	border-left:1px solid #e0e0e0;
	word-break: break-all;
}
.wxParse-td:last{
	border-top:1px solid #e0e0e0;
}
.wxParse-th{
	background:#f0f0f0;
	border-top:1px solid #e0e0e0;
}
.wxParse-del{
    display: inline;
}
.wxParse-figure {
  overflow: hidden;
}
</style>