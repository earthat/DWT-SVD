function  [finalwatermrked,U11,V11]=embedding(P,A,watermark,signalinframe,iter,dwtlevel)
cnt=1;% initilaisation of counter variable
ind=1; % counter started to pick the element from the original image vector
gain=P;
if numel(gain)==1
    gain=P*ones(1,iter);
end
for ii=1:iter
    frame=A(cnt:signalinframe*ii);
     temp=frame;
    for jj=1:dwtlevel
        [cA{jj},cD{jj}]=dwt(temp,'haar');
        temp=cD{jj};
    end
    clear temp
    % converting into vectorform
    temp=cD{1};
    for jj=1:dwtlevel-1
        temp=cat(1,temp,cD{jj+1});
    end
    vectorform=[cA{dwtlevel}' flipud(temp)'];
    clear temp
    
    % making matrix D as shown in Ref paper in figure 6 
    D=cD{1}';
    for jj=1:dwtlevel-1
%         temp=(cat(1,cD{jj+1},cD{jj+1}))';
        temp=repmat(cD{jj+1}',[1,2^jj]);
        D=cat(1,D,temp(1:size(D,2)));
    end
    % calculation of SVD
    [U,S,V] = svd(D,'econ');
    
    % conversion of watremark bits into same size of matrix as S at non
    % diagonal psoition
    temp=watermark(1:size(S,1)-dwtlevel);
    W=zeros(dwtlevel);
    cnt1=1;
    
    %since diagonal element positions are at a distnace of (dwtlevel+1)from
    %each other, so loop variable will be compared with that psoition like ( kk+1==cnt1+dwtlevel+1; ) 
    %and zero is placed at that position
    for kk=1:dwtlevel^2-1
        if kk+1==cnt1+dwtlevel+1; 
            W(kk+1)=0;
            counter=1;
        else
            W(kk+1)=watermark(ind);
            ind=ind+1;
        end
        if exist('counter','var')
            cnt1=cnt1+dwtlevel+1;
            clear counter
        end
        
    end
    clear cnt1
    W=W';
    %%
    Sw=S+gain(ii)*W; % adding watermark bits to S matrix
    %%
    [U1,S1,V1] = svd(Sw,'econ');
    U11(ii,:)=reshape(U1,1,dwtlevel^2);
    V11(ii,:)=reshape(V1,1,dwtlevel^2);
    % inverse of SVD
    Dww=U*S1*V';
    
    % inverse of DWT
    colms=size(Dww,2);
    for kk=1:dwtlevel
        if kk==1|| kk==2
            Dww_cD{kk}=Dww(kk,1:colms/kk);
        else
            Dww_cD{kk}=Dww(kk,1:colms/(2^(kk-1)));
        end
    end
    temp=Dww_cD{dwtlevel};
    for jj=dwtlevel:-1:1
        if numel(cA{jj})>numel(temp)
            dim=numel(cA{jj})-numel(temp);
            temp=padarray(temp,[0,dim],'post');% padding of zeros at last to make both cA and new cD of same size
        elseif (cA{jj})<numel(temp)
            dim=numel(temp)-numel(cA{jj});
            temp=temp(1:numel(cA{jj}));
        else
            fim=numel(temp);
        end
        
        temp=idwt(cA{jj}',temp,'haar');
    end
    watermrkedframe(ii,:)=temp;
    clear temp
    cnt=signalinframe*ii+1;
end
finalwatermrked=watermrkedframe(1,:);
for ii=1:size(watermrkedframe,1)-1
    finalwatermrked=cat(2,finalwatermrked,watermrkedframe(ii+1,:));
end
