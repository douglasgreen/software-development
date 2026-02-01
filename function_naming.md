# Function Naming Standards

You are an expert software engineer tasked with maintaining API clarity and developer ergonomics. The following glossary establishes a standardized verb taxonomy for function and method naming. By adhering to these semantic signals, you create self-documenting code where the verb alone communicates intent, side effects, return types, and computational complexity. Use this as a definitive reference for naming decisions to ensure consistency across modules and teams.

---

## The Programmer's Verb Taxonomy

### 1. **Data Access & Retrieval**
Verbs that fetch data without side effects (ideally pure functions).

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **get** | Immediate, synchronous retrieval from memory or cache | `getUser()`, `getConfig()` |
| **fetch** | Asynchronous retrieval over network or I/O boundary | `fetchData()`, `fetchRemoteConfig()` |
| **retrieve** | Complex lookup with potential processing overhead | `retrieveHistoricalData()` |
| **load** | Bulk retrieval into working memory/active state | `loadFile()`, `loadDataset()` |
| **read** | Consumption of stream or buffer content | `readStream()`, `readBuffer()` |
| **find** | Search returning single result or null/undefined | `findById()`, `findUser()` |
| **search** | Query returning collection of matches | `searchProducts()`, `searchKeywords()` |
| **query** | Structured data retrieval (often database/SQL) | `queryDatabase()`, `querySelector()` |
| **lookup** | Key-based retrieval from map/dictionary | `lookupCache()`, `lookupSymbol()` |
| **resolve** | Promise/settlement of async value or path | `resolvePath()`, `resolveDependency()` |

### 2. **Mutation & State Change**
Verbs indicating data modification or side effects.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **set** | Direct assignment or replacement | `setName()`, `setOptions()` |
| **update** | Partial modification preserving identity | `updateRecord()`, `updateState()` |
| **modify** | Alteration with potential structural change | `modifySchema()`, `modifyHeaders()` |
| **edit** | User-initiated content change | `editDocument()`, `editProfile()` |
| **change** | Toggle between predefined states | `changeStatus()`, `changeMode()` |
| **assign** | Allocation of reference or value | `assignRole()`, `assignId()` |
| **replace** | Complete substitution of entity | `replaceChild()`, `replaceToken()` |
| **swap** | Exchange between two entities | `swapElements()`, `swapBuffers()` |
| **reset** | Return to initial/default state | `resetForm()`, `resetCounter()` |
| **clear** | Removal of all contents/selections | `clearCache()`, `clearScreen()` |

### 3. **Creation & Construction**
Verbs that instantiate or generate new entities.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **create** | General instantiation with side effects | `createUser()`, `createFile()` |
| **make** | Factory pattern construction | `makeRequest()`, `makeObservable()` |
| **build** | Step-by-step assembly (often Builder pattern) | `buildQuery()`, `buildTree()` |
| **generate** | Algorithmic production of data/IDs | `generateUUID()`, `generateReport()` |
| **construct** | Complex object assembly with dependencies | `constructMatrix()`, `constructPayload()` |
| **initialize** / **init** | Setup of ready-to-use state | `initializeApp()`, `initModule()` |
| **instantiate** | Runtime creation from class/template | `instantiateClass()`, `instantiateComponent()` |
| **clone** | Deep copy of existing entity | `cloneObject()`, `cloneNode()` |
| **copy** | Shallow duplication | `copyArray()`, `copyFile()` |
| **derive** | Creation based on existing data transformation | `deriveKey()`, `deriveState()` |

### 4. **Deletion & Cleanup**
Verbs for removal and resource disposal.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **delete** | Permanent removal (often irreversible) | `deleteRecord()`, `deleteFile()` |
| **remove** | Extraction from collection without destruction | `removeItem()`, `removeClass()` |
| **destroy** | Complete teardown with resource cleanup | `destroySession()`, `destroyComponent()` |
| **dispose** | Release of managed resources (memory handles) | `disposeConnection()`, `disposeSubscription()` |
| **drop** | Database/structural removal | `dropTable()`, `dropIndex()` |
| **purge** | Aggressive cache/temporary cleanup | `purgeCache()`, `purgeOldLogs()` |
| **erase** | Secure/overwrite deletion | `eraseDisk()`, `eraseData()` |
| **unset** | Removal of property/variable binding | `unsetVariable()`, `unsetFlag()` |
| **close** | Termination of handle/stream | `closeFile()`, `closeSocket()` |
| **teardown** | Systematic reversal of setup | `teardownTests()`, `teardownEnvironment()` |

### 5. **Transformation & Conversion**
Verbs that input data and output new representation.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **convert** | Type or format change (A → B) | `convertCurrency()`, `convertToJSON()` |
| **transform** | Structural or semantic alteration | `transformData()`, `transformStream()` |
| **parse** | String → Structured data | `parseJSON()`, `parseDate()` |
| **stringify** | Structured data → String | `stringifyObject()`, `stringifyQuery()` |
| **serialize** | Object → Storable/transmittable format | `serializeState()`, `serializeForm()` |
| **deserialize** | Reverse of serialize | `deserializePayload()`, `deserializeConfig()` |
| **format** | Human-readable presentation | `formatDate()`, `formatNumber()` |
| **cast** | Coercive type conversion | `castToString()`, `castArray()` |
| **map** | Element-wise transformation | `mapValues()`, `mapResults()` |
| **flatten** | Nested → Flat structure | `flattenArray()`, `flattenTree()` |
| **normalize** | Standardization to canonical form | `normalizeData()`, `normalizeVector()` |
| **compress** / **decompress** | Size reduction/expansion | `compressImage()`, `decompressData()` |
| **encode** / **decode** | Representation translation | `encodeBase64()`, `decodeURIComponent()` |

### 6. **Validation & Assertion**
Verbs that check conditions and return boolean or throw.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **validate** | Comprehensive constraint checking (throws/errors) | `validateInput()`, `validateSchema()` |
| **verify** | Confirmation of correctness/truth | `verifyToken()`, `verifySignature()` |
| **check** | Lightweight condition inspection | `checkAvailability()`, `checkBounds()` |
| **ensure** | Assertion with auto-correction or throw | `ensureDirectory()`, `ensureArray()` |
| **assert** | Development-time invariant checking (throws if false) | `assertEqual()`, `assertNotNull()` |
| **is** / **has** / **can** / **should** | Boolean predicate prefixes | `isValid()`, `hasPermission()`, `canEdit()`, `shouldUpdate()` |
| **exists** | Presence verification | `existsSync()`, `fileExists()` |
| **matches** | Pattern/regression testing | `matchesRegex()`, `matchesPattern()` |
| **contains** / **includes** | Membership testing | `containsKey()`, `includesValue()` |
| **equals** | Equality comparison | `equalsIgnoreCase()`, `deepEquals()` |

### 7. **Execution & Invocation**
Verbs that trigger processes or callbacks.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **run** | General execution of task/process | `runTests()`, `runQuery()` |
| **execute** | Formal/structured command execution | `executeCommand()`, `executeTransaction()` |
| **perform** | Action with potential side effects | `performCleanup()`, `performSearch()` |
| **invoke** | Direct function/method calling | `invokeMethod()`, `invokeCallback()` |
| **call** | Immediate synchronous execution | `callFunction()`, `callHook()` |
| **apply** | Execution with context/argument binding | `applyMiddleware()`, `applyChanges()` |
| **dispatch** | Event/action routing to handlers | `dispatchEvent()`, `dispatchAction()` |
| **trigger** | Initiation of event/cascade | `triggerUpdate()`, `triggerAnimation()` |
| **emit** | Broadcasting event/signal | `emitEvent()`, `emitChange()` |
| **fire** | Immediate callback invocation | `fireCallback()`, `fireTimer()` |
| **handle** | Event processing entry point | `handleClick()`, `handleError()` |
| **process** | Systematic data handling pipeline | `processPayment()`, `processQueue()` |

### 8. **Calculation & Computation**
Verbs for deterministic mathematical/logical operations.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **calculate** | Mathematical derivation | `calculateSum()`, `calculateDistance()` |
| **compute** | Algorithmic processing | `computeHash()`, `computeLayout()` |
| **determine** | Logical deduction of state/value | `determineWinner()`, `determineOptimalPath()` |
| **evaluate** | Expression/condition resolution | `evaluateExpression()`, `evaluatePolicy()` |
| **derive** | Deduction from existing values | `deriveColor()`, `deriveKey()` |
| **estimate** | Approximation/prediction | `estimateTime()`, `estimateSize()` |
| **measure** | Physical quantity assessment | `measureText()`, `measurePerformance()` |
| **count** | Quantification | `countLines()`, `countOccurrences()` |
| **sum** | Aggregation | `sumValues()`, `sumTotal()` |
| **average** / **avg** | Mean calculation | `averageScores()`, `avgTemperature()` |
| **aggregate** | Collection summarization | `aggregateData()`, `aggregateStats()` |
| **reduce** | Fold operation (functional) | `reduceArray()`, `reduceState()` |

### 9. **Collection Operations**
Verbs specific to array/list/map manipulations.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **add** | General inclusion | `addItem()`, `addEventListener()` |
| **insert** | Placement at specific index/position | `insertRow()`, `insertBefore()` |
| **append** | Addition to end | `appendChild()`, `appendData()` |
| **prepend** | Addition to beginning | `prependHeader()`, `prependItem()` |
| **push** / **pop** | Stack operations | `pushState()`, `popElement()` |
| **shift** / **unshift** | Queue operations | `shiftQueue()`, `unshiftItem()` |
| **concat** | Concatenation | `concatArrays()`, `concatStrings()` |
| **merge** | Deep combination (often objects) | `mergeObjects()`, `mergeConfigs()` |
| **join** | Connection with separator | `joinPath()`, `joinQueryParams()` |
| **split** | Separation by delimiter | `splitString()`, `splitChunks()` |
| **slice** | Extraction of sub-range | `sliceArray()`, `sliceBuffer()` |
| **splice** | Removal/replacement at index | `spliceArray()` |
| **filter** | Conditional subset selection | `filterActive()`, `filterByType()` |
| **select** | Specific item picking | `selectFields()`, `selectOptions()` |
| **distinct** / **unique** | Duplicate elimination | `distinctValues()`, `uniqueIds()` |
| **group** | Categorization by key | `groupByCategory()`, `groupResults()` |
| **partition** | Binary splitting | `partitionArray()`, `partitionData()` |
| **sort** | Ordering arrangement | `sortByDate()`, `sortDescending()` |
| **reverse** | Order inversion | `reverseArray()`, `reverseString()` |
| **shuffle** | Random reordering | `shuffleDeck()`, `shuffleArray()` |
| **zip** | Interleaving of collections | `zipArrays()`, `zipFiles()` |
| **flatten** | Nested to flat | `flattenHierarchy()` |

### 10. **I/O & Network Operations**
Verbs for external system communication.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **read** | Input stream consumption | `readFile()`, `readStream()` |
| **write** | Output to destination | `writeFile()`, `writeResponse()` |
| **save** | Persistent storage | `saveDocument()`, `saveSettings()` |
| **download** | Network → Local storage | `downloadImage()`, `downloadBlob()` |
| **upload** | Local → Remote storage | `uploadFile()`, `uploadData()` |
| **send** | Transmission to recipient | `sendEmail()`, `sendRequest()` |
| **receive** | Incoming data acceptance | `receiveMessage()`, `receivePacket()` |
| **post** | HTTP POST / message posting | `postData()`, `postMessage()` |
| **put** | HTTP PUT / idempotent update | `putResource()`, `putRecord()` |
| **patch** | HTTP PATCH / partial update | `patchDocument()`, `patchEntity()` |
| **subscribe** / **unsubscribe** | Event stream registration | `subscribeTopic()`, `unsubscribeChannel()` |
| **connect** / **disconnect** | Connection lifecycle | `connectDatabase()`, `disconnectSocket()` |
| **listen** | Port/event waiting | `listenPort()`, `listenEvents()` |
| **accept** | Incoming connection handling | `acceptConnection()` |

### 11. **Lifecycle & State Management**
Verbs for component/system state transitions.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **setup** | Initial configuration | `setupServer()`, `setupListeners()` |
| **configure** | Parameter adjustment | `configureOptions()`, `configureStore()` |
| **prepare** | Readiness operations | `prepareData()`, `prepareEnvironment()` |
| **start** | Initiation of operation | `startEngine()`, `startTimer()` |
| **stop** | Cessation of operation | `stopProcess()`, `stopAnimation()` |
| **pause** / **resume** | Temporary suspension | `pauseVideo()`, `resumeStream()` |
| **enable** / **disable** | Capability toggling | `enableFeature()`, `disableButton()` |
| **activate** / **deactivate** | Focus/primary state toggling | `activateTab()`, `deactivateModule()` |
| **show** / **hide** | Visibility control | `showModal()`, `hideLoading()` |
| **open** / **close** | Access state control | `openConnection()`, `closeDialog()` |
| **lock** / **unlock** | Access restriction | `lockFile()`, `unlockMutex()` |
| **toggle** | Binary state switching | `toggleVisibility()`, `toggleSwitch()` |
| **mount** / **unmount** | DOM/Runtime attachment | `mountComponent()`, `unmountApp()` |
| **bootstrap** | System initialization | `bootstrapApp()`, `bootstrapModule()` |

### 12. **Asynchronous & Concurrency Control**
Verbs specific to timing and parallel execution.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **async** | Asynchronous operation marker | `asyncLoad()`, `asyncProcess()` |
| **await** | Promise resolution waiting | `awaitResult()`, `awaitCondition()` |
| **defer** | Delayed execution | `deferUpdate()`, `deferCalculation()` |
| **delay** | Time-based postponement | `delayExecution()`, `delayRetry()` |
| **schedule** | Timed execution planning | `scheduleTask()`, `scheduleJob()` |
| **queue** | FIFO ordering | `queueAction()`, `queueRequest()` |
| **throttle** | Rate limiting (time-based) | `throttleScroll()`, `throttleInput()` |
| **debounce** | Group rapid calls into one | `debounceSearch()`, `debounceResize()` |
| **retry** | Failure recovery attempt | `retryOperation()`, `retryFetch()` |
| **timeout** | Execution time limiting | `timeoutRequest()`, `timeoutPromise()` |
| **cancel** | Abortion of pending operation | `cancelRequest()`, `cancelAnimation()` |
| **abort** | Forceful termination | `abortController()`, `abortFetch()` |
| **wait** | Blocking/delaying | `waitFor()`, `waitUntil()` |
| **sync** / **synchronize** | State alignment | `syncData()`, `synchronizeTime()` |

### 13. **Testing & Quality Assurance**
Verbs for verification and test construction.

| Verb | Signal | Typical Pattern |
|------|--------|----------------|
| **test** | Execution of test case | `testFunctionality()`, `testEdgeCase()` |
| **mock** | Fake implementation creation | `mockApi()`, `mockFunction()` |
| **stub** | Placeholder method replacement | `stubMethod()`, `stubResponse()` |
| **spy** | Observation wrapper | `spyOnMethod()`, `spyConsole()` |
| **assert** | Expectation verification | `assertTrue()`, `assertThrows()` |
| **expect** | Assertion declaration (BDD style) | `expectValue()`, `expectError()` |
| **given** | Precondition setup (Gherkin) | `givenUser()`, `givenData()` |
| **when** | Action trigger (Gherkin) | `whenClicking()`, `whenSubmitting()` |
| **then** | Outcome verification (Gherkin) | `thenResult()`, `thenError()` |
| **arrange** / **act** / **assert** | AAA pattern | `arrangeData()`, `actOnTarget()` |
| **verify** | Mock interaction checking | `verifyCalled()`, `verifyParams()` |
| **snapshot** | Regression capture | `snapshotComponent()`, `snapshotState()` |
| **benchmark** | Performance measurement | `benchmarkSort()`, `benchmarkApi()` |
| **fuzz** | Randomized input testing | `fuzzInput()`, `fuzzParser()` |

---

## Composition Guidelines

**Prefix Modifiers** (use to refine core verbs):
- `try` (e.g., `tryParse`, `tryLock`) - Attempt without throwing
- `re` (e.g., `retry`, `reload`, `refresh`) - Repetition/re-execution
- `pre` / `post` (e.g., `preprocess`, `postprocess`) - Temporal positioning
- `un` (e.g., `undo`, `unwrap`) - Reversal/extraction

**Suffix Patterns**:
- `By` (e.g., `sortByDate`, `groupById`) - Specifies discriminator
- `From` (e.g., `loadFromCache`, `readFromFile`) - Specifies source
- `To` (e.g., `convertToString`, `saveToDisk`) - Specifies destination
- `With` (e.g., `mergeWithDefaults`, `compareWithPrevious`) - Specifies context
- `Async` (e.g., `loadAsync`, `validateAsync`) - Explicit async marker

---

## Anti-Patterns to Avoid

1. **Ambiguous Synonym Mixing**: Don't use both `remove` and `delete` interchangeably; establish distinct semantics (e.g., `remove` from collection vs `delete` from database).

2. **Getter Side Effects**: Never use `get` for operations that modify state. Use `fetch`, `load`, or `create` instead.

3. **Boolean without Prefix**: Functions returning booleans should use `is`, `has`, `can`, or `should` prefixes, not bare adjectives (use `isEmpty()` not `empty()`).

4. **Noun-Verbing**: Avoid turning nouns into verbs (e.g., `componentize`, `objectify`) when standard alternatives exist.

5. **Overloaded Context**: Avoid `process` when a more specific verb (transform, validate, parse) applies.

Apply these verbs as semantic contracts: once a verb signals a specific behavior in your codebase, maintain that contract consistently across all modules.
