import wepy from 'wepy'

export default class util extends wepy.mixin {
  // 手机号码正则验证
  checkPhone (tel) {
    console.log(tel)
    if (!(/^1[3456789]\d{9}$/.test(tel))) {
      return false
    }
    return true
  }

  reSort(arr) {
    let temp = [[], [], []]
    let t = []
    for (let o of arr) {
      if (o.return_visit === 0 && !o.id) {
        temp[0].push(o)
      }
      if (o.return_visit === 1 && !o.id) {
        temp[1].push(o)
      }
      if (o.id) {
        temp[2].push(o)
      }
    }
    t = t.concat(temp[0]).concat(temp[1]).concat(temp[2])
    return t
  }

  // 排序
  fixedData(arr) {

  }

  partition(arr, low, high) {
    let middle = arr[high]
    let i = low - 1
    for (let j = low; j < high; j++) {
      if (!middle.id) {
        if (!arr[j].id) {
          if (arr[j].return_visit < middle.return_visit) {
            i++
            this.swap(arr, i, j)
          } else if (arr[j].return_visit === middle.return_visit) {
            if (arr[j].return_visit === 0) {
              if (i < high) {
                i++
                this.swap(arr, i, j)
              }
            } else {

            }
          }
        } else {

        }
      }
    }
  }

  swap(arr, i, j) {
    let t = arr[j]
    arr[j] = arr[i]
    arr[i] = t
  }

  // 扫码
  shareCode () {
    let that = this
    // 判断是否授权摄像头
    wx.getSetting({
      success: res => {
        // 未授权让用户授权
        if (!res.authSetting['scope.camera']) {
          wx.authorize({
            scope: 'scope.camera',
            success () {
              wx.scanCode({
                success (res) {
                  that.signInApi(res.result).then(data => {
                    console.log(data, 111)
                    let Data = data.data.data
                    if (data.data.resultCode === 1000) {
                      that.$navigate('./signOk',
                        {
                          user_name: Data.user.user_name,
                          icon: Data.user.icon,
                          village_name: Data.user.villageInfo.village_name,
                          door_number: Data.user.userAut.door_number
                        }
                      )
                    } else {
                      console.log(data.data)
                      that.$navigate('./lose', {error: data.data.error})
                    }
                  })
                }
              })
            },
            // 拒绝授权处理
            fail () {
              console.log('用户拒绝授权')
            }
          })
        } else {
          wx.scanCode({
            success (res) {
              that.signInApi(res.result).then(data => {
                console.log(data, 111)
                let Data = data.data.data
                console.log(Data)
                if (data.data.resultCode === 1000) {
                  that.$navigate('./signOk',
                    {
                      user_name: Data.user.user_name,
                      icon: Data.user.icon,
                      village_name: Data.user.villageInfo.village_name,
                      door_number: Data.user.userAut.door_number
                    }
                  )
                } else {
                  console.log(data.data)
                  that.$navigate('./lose', {error: data.data.error})
                }
              })
            }
          })
        }
      }
    })
  }
}
