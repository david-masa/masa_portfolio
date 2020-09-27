<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  asyncData({params}) {
    return Promise.all([
      client.getEntries({
        'content_type': 'work',
        'fields.slug': params.slug // 取得対象をslugフィールドがURL内のslugパラメータと等しいものに限定
      })
    ]).then(([works]) => {
      return {
        work: works.items[0] // 取得した配列データの初めの１つを変数workに入れる
      }
    }).catch(console.error)
  }
}
</script>