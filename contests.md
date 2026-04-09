# 比赛 API

## 列出比赛

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>GET /contest/list</code></td>
  </tr>
  <tr>
    <th align="right">参数</th>
    <td>
      <code>{ page?: number, method?: number, public?: number, name?: string }</code><br>
      <code>method</code> 赛制。1: OI, 2: ICPC, 3: 乐多, 4: IOI。未提供时为全部。<br>
      <code>public</code> 分类。1: 官方比赛, 2: 团队公开赛, 4: 个人公开赛, 11: 重现赛。未提供时为全部。<br>
      <code>name</code> 比赛名称或者编号。
    </td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>LentilleDataResponse&lt;{ contests: List&lt;Contest&gt; }&gt;</code>)</td>
  </tr>
</table>

## 列出参加的比赛

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>GET /api/user/joinedContests</code></td>
  </tr>
  <tr>
    <th align="right">参数</th>
    <td><code>{ page?: number }</code></td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>{ contests: List&lt;Contest&gt; }</code>)</td>
  </tr>
</table>

## 列出创建的比赛

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>GET /api/user/createdContests</code></td>
  </tr>
  <tr>
    <th align="right">参数</th>
    <td><code>{ page?: number }</code></td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>{ contests: List&lt;Contest&gt; }</code>)</td>
  </tr>
</table>

## 获取比赛

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>GET /contest/:id</code></td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>LentilleDataResponse&lt;ContestData&gt;</code>)</td>
  </tr>
</table>

## 获取创建的比赛

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>GET /contest/edit/:id</code></td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>DataResponse&lt;CreatedContestData&gt;</code>)</td>
  </tr>
</table>

## 获取排行榜

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>GET /fe/api/contest/scoreboard/:id</code></td>
  </tr>
  <tr>
    <th align="right">参数</th>
    <td><code>{ page?: number }</code></td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>GetScoreboardResponse</code>)</td>
  </tr>
</table>

## 参加比赛

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>POST /contest/:id/join</code> （或 <code>POST /fe/api/contest/join/:id</code>）</td>
  </tr>
  <tr>
    <th align="right">请求主体</th>
    <td><code>application/json</code> (<code>{ code?: string; unrated?: boolean; squadCode?: string }</code>)<br>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>{ id: number }</code>)</td>
  </tr>
</table>

## 创建小队

用于在允许组队的比赛中创建一个小队（当前用户自动成为队长）。

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>POST /contest/:id/squad</code></td>
  </tr>
  <tr>
    <th align="right">请求主体</th>
    <td><code>application/json</code> (<code>{}</code>)</td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>{ squad: SquadDetails }</code>)</td>
  </tr>
</table>

## 退出小队/踢出队员/解散小队

退出当前所在的小队，或由队长踢出指定队员。如果队长自己退出，则等于解散整个小队。

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>POST /contest/:id/squadMemberQuit</code></td>
  </tr>
  <tr>
    <th align="right">请求主体</th>
    <td><code>application/json</code> (<code>{ uid: number }</code>)<br>
    <code>uid</code></td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>{ squad: SquadDetails | null }</code>) 
  </tr>
</table>

## 创建比赛

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>POST /fe/api/contest/new</code></td>
  </tr>
  <tr>
    <th align="right">请求主体</th>
    <td><code>application/json</code> (<code>EditContestRequest</code>)</td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>{ id: number }</code>)</td>
  </tr>
</table>

## 编辑比赛

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>POST /fe/api/contest/edit/:id</code></td>
  </tr>
  <tr>
    <th align="right">请求主体</th>
    <td><code>application/json</code> (<code>EditContestRequest</code>)</td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>{ id: number }</code>)</td>
  </tr>
</table>

## 编排比赛题目

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>POST /fe/api/contest/editProblem/:id</code></td>
  </tr>
  <tr>
    <th align="right">请求主体</th>
    <td><code>application/json</code> (<code>{ pids: string[]; scores: { [pid: string]: number } }</code>)</td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>{}</code>)</td>
  </tr>
</table>

## 删除比赛

<table>
  <tr>
    <th align="right">请求</th>
    <td><code>POST /fe/api/contest/delete/:id</code></td>
  </tr>
  <tr>
    <th align="right">响应主体</th>
    <td><code>application/json</code> (<code>{}</code>)</td>
  </tr>
</table>
