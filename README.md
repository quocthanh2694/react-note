# Reactjs

## Use interact params between Container and Child 
```
// Define Container
const Container = ({children})=>{
    const [paramA, setParamA] = useState(false);

    const changeParamA = ()=>{
        setParamA(!paramA);
    }

    return children({paramA, changeParamA});
};


/// In main
<Container>
{
    (paramA, changeParamA)=>{
        return <Div>
            <div>Param status: {paramA}</div>
            <div onClick={changeParamA}>A</div>
        </Div>
    }
}
</Container>
```

